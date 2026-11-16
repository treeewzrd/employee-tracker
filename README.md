# Employee Tracker

**Coursework / learning project**

A terminal application for managing departments, roles, and employees in PostgreSQL. Built to practice TypeScript, relational database design, SQL joins, parameterized queries, and interactive command-line menus.

[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](LICENSE)

## What the application does

- Lists employees, roles, and departments.
- Filters employees by department or manager.
- Adds and removes employees, roles, and departments.
- Updates an employee's role or manager.
- Calculates department salary totals from employee roles.

This is a coursework reference, not a production human-resources system. Use sample data.

## Stack

TypeScript, Node.js, PostgreSQL, node-postgres (`pg`), Inquirer, dotenv, and asciiart-logo.

## Local setup

Requirements: Node.js with npm, a running local PostgreSQL server, and the PostgreSQL `psql` client. A currently supported Node.js version is preferable; this cleanup has not established a tested runtime version.

### 1. Download and install dependencies

```bash
git clone https://github.com/treeewzrd/EMPLOYEE-TRACKER.git
cd EMPLOYEE-TRACKER
npm ci
```

### 2. Configure your private environment

For an existing local checkout, preserve your current credentials privately before pulling changes that remove the previously tracked `.env` file. Do not overwrite an existing working `.env` with the example.

For a new checkout:

```bash
cp .env.example .env
```

Edit the root `.env` file:

```dotenv
DB_NAME=employees
DB_USER=your_database_user
DB_PASSWORD=your_unique_local_password
```

The application loads `DB_NAME`, `DB_USER`, and `DB_PASSWORD` through dotenv. Its current connection code fixes the host to `localhost` and port to `5432`; `DB_HOST` and `DB_PORT` do not override them.

Use a local PostgreSQL role appropriate for this exercise. The initialization script requires permission to create and drop the exercise database. Keep credentials out of Git, and replace any password previously published in repository history.

### 3. Initialize a disposable database

**The existing schema script drops and recreates a database named `employees`. It erases any existing data in that database.** Review [schema.sql](src/db/schema.sql) before running it. Do not use it against a database containing data you need to keep.

On a local development instance where `employees` is reserved for this exercise, run the following from the repository root. Replace `your_database_user` with your PostgreSQL role; `-W` prompts privately for its password.

```bash
psql -h localhost -U your_database_user -d postgres -W -v ON_ERROR_STOP=1 -f src/db/schema.sql
```

Optionally load the sample departments, roles, and employees into the newly initialized database:

```bash
psql -h localhost -U your_database_user -d employees -W -v ON_ERROR_STOP=1 -f src/db/seed.sql
```

Both SQL scripts explicitly target `employees`. Changing only `DB_NAME` does not retarget these scripts. The seed script is intended for a fresh schema; repeated runs are not a reset mechanism.

### 4. Build and start

Run from the repository root so dotenv can find `.env`:

```bash
npm run build
npm start
```

The build compiles `src/` into `dist/`. Start runs `dist/index.js`; rebuild after changing TypeScript source.

## Usage

Use the arrow keys and Enter to choose an action from the Employee Manager menu. Create departments before roles, then create employees using those roles. Choose **Quit** to exit.

Deleting a department also deletes its roles and employees. Deleting a role also deletes employees assigned to it. Deleting a manager leaves their reports with no manager, following the schema's foreign-key rules.

## Verification

During the documentation cleanup, the commands and configuration above were checked against `package.json`, the database connection code, the SQL scripts, and the menu implementation.

Dependency installation, compilation, and interactive database behavior were **not executed** during that review. The repository's `npm test` command is a placeholder that exits with an error; it does not run an automated test suite.

To verify a local setup using disposable sample data:

1. Build and start the application.
2. View departments, roles, and employees.
3. Add a sample department, role, and employee.
4. Change that employee's role and manager, then verify the displayed values.
5. Check department salary totals.
6. Delete only the sample records and confirm the results.

## Project files

| Path | Purpose |
| --- | --- |
| [src/index.ts](src/index.ts) | Interactive menu and prompts |
| [src/db/index.ts](src/db/index.ts) | Parameterized database operations |
| [src/db/connection.ts](src/db/connection.ts) | PostgreSQL connection pool |
| [src/db/schema.sql](src/db/schema.sql) | Destructive exercise database initialization |
| [src/db/seed.sql](src/db/seed.sql) | Sample records |
| [.env.example](.env.example) | Safe configuration template |
| [package.json](package.json) | Dependencies and run commands |

## License

[ISC](LICENSE). Maintained publicly as coursework by [treeewzrd](https://github.com/treeewzrd).
