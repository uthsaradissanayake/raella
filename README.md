[README.md](https://github.com/user-attachments/files/22364328/README.md)
# Seafarer SRS Monorepo

Offline-first spaced repetition platform for seafarers, aligned with Anki formats and FSRS.

## Structure
```
apps/
  api/   # NestJS + Prisma + PostgreSQL + Redis + S3 presign stub
  web/   # Next.js (app router) + React Query + Dexie (IndexedDB) + PWA shell
packages/
  fsrs/      # FSRS scheduler (TypeScript) + vitest unit tests
  shared/    # zod schemas, shared types/helpers
```

## Requirements
- Node 18+
- npm 9+ (or pnpm/yarn if you prefer)
- PostgreSQL 14+
- (Optional) Redis, MinIO/S3 for presigned URLs

## Quick Start

### 1) Install deps
```bash
npm install
```

### 2) Environment
Copy example env files and adjust:
```bash
cp apps/api/.env.example apps/api/.env
cp apps/web/.env.example apps/web/.env
```

### 3) Database
```bash
# In one terminal (ensure Postgres running and DATABASE_URL in apps/api/.env)
npm run prisma:generate
npm run prisma:migrate
```

### 4) Run dev (separate terminals or run concurrently)
```bash
npm run dev:api
npm run dev:web
```

- API: http://localhost:4000
- Web: http://localhost:3000

### 5) Tests
```bash
npm test
```

## Notes
- This is a minimal scaffold. Fill in real implementations, security hardening, and production infra (Terraform, CI/CD).
- FSRS implementation is simplified and deterministic for initial testing; replace/extend with full FSRS as needed.


## New Features in this drop
- Auth (register/login) + device registration
- Review ops with idempotency and FSRS computation
- Due-card selector endpoint
- Redis queues + BullMQ workers for .apkg import/export (scaffold level)
- Real S3 presign using AWS SDK v3
- Web Review Runner (minimal) at `/review`
- Mobile Expo app with offline outbox

### Extra setup
- Set `REDIS_URL` and run Redis
- For workers, run Node process importing `import.worker.ts` and `export.worker.ts` (ts-node or build)
- Provide S3 credentials to use presign endpoints
