# Prisma Compute deploy example

A small [Hono](https://hono.dev) REST API using Prisma ORM and Prisma
Postgres, ready to deploy to Prisma Compute with one click.

## Deploy

[**Deploy to Prisma Compute**](https://console.prisma.io/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fprisma%2Fcompute-deploy-example)

Clicking the link copies this repository into a new repository under your
GitHub account, provisions a Prisma Postgres database, sets `DATABASE_URL`
for you, and starts the first deployment. After that, every push to your
copy's default branch deploys automatically.

## What makes this repository deployable

Prisma Compute deploys any public TypeScript repository that has these files
at its root:

- `prisma.compute.json` — tells Prisma Compute how to run the app
- `package.json`
- a lockfile (`bun.lock`, `package-lock.json`, `pnpm-lock.yaml`, or `yarn.lock`)

## Run locally

```bash
bun install
cp .env.example .env

# Authenticate once, then create a Prisma Postgres database.
bun run compute:login
bun run compute:database:create

# Copy the printed DATABASE_URL into .env.

bun run db:generate
bun run db:migrate --name init
bun run db:seed
bun run dev
```

Open [http://localhost:8080](http://localhost:8080). The JSON endpoint is
available at [http://localhost:8080/api/users](http://localhost:8080/api/users).
