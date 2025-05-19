# Employee Tracker

[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](https://opensource.org/licenses/ISC)
[![Node.js](https://img.shields.io/badge/Node.js-18%2B-brightgreen)](https://nodejs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-14%2B-blue)](https://www.postgresql.org/)
[![Inquirer](https://img.shields.io/badge/Inquirer-8.2.4-yellow)](https://www.npmjs.com/package/inquirer/v/8.2.4)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.2.2-blue)](https://www.typescriptlang.org/)

A command-line Content Management System (CMS) for managing a company's employee database, built with Node.js, TypeScript, Inquirer, and PostgreSQL.

---

## Table of Contents

- [Features](#features)
- [Demo Video](#demo-video)
- [Installation](#installation)
- [Usage](#usage)
- [Database Schema](#database-schema)
- [Project Structure](#project-structure)
- [Technologies Used](#technologies-used)
- [License](#license)

---

## Features

- View all departments, roles, and employees
- Add new departments, roles, and employees
- Update employee roles and managers
- View employees by department or manager
- Delete departments, roles, and employees
- View total utilized budget by department

---

## Demo Video

> 📹 **Demo Video:**  
> [Watch the Screencastify Demo](https://app.screencastify.com/v2/watch/JhRsX9KFJvd7oDodaLS9)  

---

## Installation

1. **Clone the repository:**
   ```sh
   git clone https://github.com/your-username/employee-tracker.git
   cd employee-tracker

2. **Install dependencies:*
   npm install

3. **Configure environmental variables**
    Copy .env.example to .env and fill in your PostgreSQL credentials:

    DB_NAME=employees DB_USER=your_db_user 
    DB_PASSWORD=your_db_password 
    DB_HOST=localhost DB_PORT=5432

4. **Set up the database:**
    Ensure PostgreSQL is running.
    Run the schema and seed scripts:

    psql -U your_db_user -f [schema.sql](http://_vscodecontentref_/0)
    psql -U your_db_user -f  [seed.sql](http://_vscodecontentref_/1)

5. **Build the project**
    npm run build

6. **Start the application:**
    npm start

## Usage
On launch, you'll see an ASCII logo and a menu of actions.
Use arrow keys to navigate and select options.
Follow prompts to view, add, update, or delete data.
To exit, select "Quit" from the menu.

## Database Schema
The application uses three main tables:

department
    id (SERIAL PRIMARY KEY)
    name (VARCHAR(30) UNIQUE NOT NULL)
role
    id (SERIAL PRIMARY KEY)
    title (VARCHAR(30) UNIQUE NOT NULL)
    salary (DECIMAL NOT NULL)
    department_id (INTEGER NOT NULL, FOREIGN KEY)
employee
    id (SERIAL PRIMARY KEY)
    first_name (VARCHAR(30) NOT NULL)
    last_name (VARCHAR(30) NOT NULL)
    role_id (INTEGER NOT NULL, FOREIGN KEY)
    manager_id (INTEGER, FOREIGN KEY, nullable)

## Project Structure

employee-tracker/
├── src/
│   ├── [index.ts](http://_vscodecontentref_/2)               # Main CLI application
│   ├── db/
│   │   ├── [connection.ts](http://_vscodecontentref_/3)      # PostgreSQL connection setup
│   │   ├── [index.ts](http://_vscodecontentref_/4)           # Database query class
│   │   ├── [schema.sql](http://_vscodecontentref_/5)         # Database schema
│   │   └── [seed.sql](http://_vscodecontentref_/6)           # Seed data
│   └── types/
│       └── [asciiart-logo.d.ts](http://_vscodecontentref_/7) # Type definitions
├── .env                      # Environment variables
├── [package.json](http://_vscodecontentref_/8)
├── [tsconfig.json](http://_vscodecontentref_/9)
└── [README.md](http://_vscodecontentref_/10)

## Technologies Used
    Node.js
    TypeScript
    Inquirer v8.2.4
    PostgreSQL
    pg
    asciiart-logo
    dotenv

## License
This project is licensed under the ISC License.