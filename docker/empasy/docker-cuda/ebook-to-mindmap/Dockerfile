# 1️⃣ 빌드 스테이지
FROM node:24-alpine AS builder

# pnpm 설치
RUN npm install -g pnpm

# 작업 디렉토리 설정
WORKDIR /app

# 패키지 파일 복사
COPY pnpm-lock.yaml package.json ./

# 의존성 설치
RUN pnpm install

# 소스 복사
COPY . .

# 빌드 (Next.js, Vite 등)
RUN pnpm run build

# 2️⃣ 실행 스테이지
FROM node:24-alpine AS runner
WORKDIR /app

RUN npm install -g pnpm

# builder에서 빌드된 결과 복사
COPY --from=builder /app ./

# 포트 노출 (Next.js/Vite 기본 포트 예시)
EXPOSE 3000

# 개발용으로 실행하고 싶을 때 (일반적으로는 pnpm run start)
CMD ["pnpm", "run", "dev"]