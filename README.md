# Employee Tracker

**Coursework for school**

![Coursework](https://img.shields.io/badge/Coursework-blue)
[![License: ISC](https://img.shields.io/badge/license-ISC-green)](LICENSE)

Coursework CLI for managing departments, roles, employees, and department salary totals.

**Built with:** TypeScript, Node.js, PostgreSQL, Inquirer.

## What I built

- Built an interactive employee-management CLI with Inquirer.
- Designed department, role, employee, and manager relationships in PostgreSQL.
- Implemented parameterized SQL for CRUD operations, filtered employee views, and department salary totals.

## Explore the source

- [src/index.ts](src/index.ts) — Interactive menus and prompts.
- [src/db/index.ts](src/db/index.ts) — Parameterized SQL operations.
- [src/db/schema.sql](src/db/schema.sql) — Relational schema.

## Run locally

Requires Node.js/npm, PostgreSQL, and `psql`. From the repository root:

```bash
npm ci
cp .env.example .env
```

Skip the copy if you already have a working `.env`. Set `DB_NAME=employees`, `DB_USER`, and `DB_PASSWORD` privately. The code currently fixes the host and port to `localhost:5432`; `DB_HOST` and `DB_PORT` are not read.

**Database setup deletes and recreates `employees`.** Use a disposable database only. Review [schema.sql](src/db/schema.sql), then initialize it with a local role permitted to create the exercise database:

```bash
psql -h localhost -U your_database_user -d postgres -W -v ON_ERROR_STOP=1 -f src/db/schema.sql
psql -h localhost -U your_database_user -d employees -W -v ON_ERROR_STOP=1 -f src/db/seed.sql
npm run build
npm start
```

Seed once on a fresh schema. Use the menu to view or edit sample records; choose **Quit** to exit. Deleting departments or roles also deletes their associated records.

## Checks

`npm test` is a placeholder. Manually check listing, adding, updating, deleting, and salary totals using sample data.

Setup instructions were checked against source; builds and application behavior have not been rerun during this cleanup.

**License:** [ISC](LICENSE).
