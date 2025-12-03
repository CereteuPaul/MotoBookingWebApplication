# MotoBooking — Motorcycle Circuit Management System 🏍️

MotoBooking is a web application for managing motorcycle circuit bookings, riders and events. This repository contains the backend server (`server.js`), frontend assets and database integration. The project is intended to be run locally with a SQL Server database (SSMS) and Node.js.

This README provides a clear overview, setup instructions, common tasks and troubleshooting steps so you can get the project running quickly. 🚀

---

## Table of contents 📚

- [Features](#features)
- [Technology stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Quick start](#quick-start)
- [Configuration](#configuration)
- [Database setup](#database-setup)
- [Run the app](#run-the-app)
- [Development tips](#development-tips)
- [Project structure](#project-structure)
- [Troubleshooting](#troubleshooting)

---

## Features ✨

- Create, view and manage circuit bookings 🗓️
- Rider and motorcycle management (register, update, list) 👤🏍️
- Admin interface for event and slot management 🛠️
- Simple web UI with server-side endpoints 🌐
- Uses SQL Server as the application database 🗄️

---

## Technology stack 🧩

- Node.js (server entry: `server.js`) 💻
- SQL Server (use SQL Server Management Studio - SSMS) 🗄️
- Frontend: HTML, CSS, JavaScript (static assets served by Node) 🎨
- Optional developer tools: nodemon, PM2 🔁

---

## Prerequisites ✅

- Node.js (recommended v14+)
- npm (comes with Node.js)
- Microsoft SQL Server and SQL Server Management Studio (SSMS)
- Git (to clone the repo)

---

## Quick start ⚡

1. Clone the repository
   ```bash
   git clone https://github.com/CereteuPaul/MotoBookingWebApplication.git
   cd MotoBookingWebApplication
   ```

2. Install dependencies
   ```bash
   npm install
   ```

3. Configure the database connection (see [Configuration](#configuration)).

4. Start the database (open SSMS, start the SQL Server instance, ensure credentials and firewall rules allow local connections). 🔌

5. Start the application:
   ```bash
   node server.js
   ```
   or, if there is an npm script:
   ```bash
   npm start
   ```

6. Open your browser and go to:
   ```
   http://localhost:3000
   ```
   (If your app uses a different PORT, open that port — see configuration.) 🌐

---

## Configuration 🔧

Create a `.env` file in the project root (if the project uses environment variables). Example variables commonly used:

```bash
PORT=3000
DB_HOST=localhost
DB_PORT=1433
DB_USER=sa
DB_PASSWORD=YourStrong@Passw0rd
DB_NAME=MotoBookingDB
```

- DB_* values must match your SQL Server instance and credentials.
- If the app reads configuration from a different place (e.g. a config file), update accordingly.

Important: Never commit real credentials to version control. Use `.gitignore` to exclude `.env`. 🔒

---

## Database setup 🗂️

If you have a SQL script for schema and seed data (e.g. `database.sql`, `schema.sql`, or a `migrations/` folder), run/import it in SSMS:

1. Open SSMS and connect to your SQL Server instance.
2. Create the database you will use (if not created by the script):
   ```sql
   CREATE DATABASE MotoBookingDB;
   GO
   ```
3. Open the provided SQL script(s) and execute them against the `MotoBookingDB` database.
4. Verify tables and initial data are present.

If there are no SQL scripts in the repository, inspect the codebase for migration or model setup instructions and follow them. If the server automatically creates tables, check server logs on first run to ensure the connection and schema initialization succeed. 🔎

---

## Run the app ▶️

- Start SQL Server and ensure you can connect using SSMS with the credentials in `.env`.
- Start the Node server:
  ```bash
  node server.js
  ```
- For development with automatic restarts:
  ```bash
  npm install -g nodemon
  nodemon server.js
  ```
- For production deployment consider using a process manager:
  ```bash
  npm install -g pm2
  pm2 start server.js --name motobooking
  ```

---

## Development tips 🛠️

- Logs: Check the console output for connection errors or runtime exceptions. 📟
- Port conflicts: If `3000` is in use, change `PORT` in `.env`. 🔁
- Use Postman or curl to test backend endpoints. 📬
- Add helpful logging in `server.js` while developing (if not already present). 📝
- If you add new environment variables, create/update `.env.example` so contributors know which values are required. 📄

---

## Project structure (suggested) 🗂️

A typical structure for reference — adapt to the actual repo layout:

- `server.js` — entry point for the server
- `package.json` — npm dependencies and scripts
- `/routes` — route handlers (bookings, users, admin)
- `/controllers` — business logic
- `/models` — database models or queries
- `/public` — frontend static assets (HTML/CSS/JS)
- `/views` — server-rendered templates (if used)
- `/migrations` or `/database` — SQL or migration scripts

---

## Troubleshooting 🐛⚠️

- "Cannot connect to SQL Server":
  - Ensure SQL Server is running.
  - Ensure the instance allows SQL authentication and the DB user exists.
  - Check firewall rules and that you use the correct host/port.
  - Verify credentials and database name in `.env`.

- "Port already in use":
  - Change `PORT` in `.env` or stop the process using that port.

- "Module not found" or dependency errors:
  - Run `npm install`.
  - If a package was added but not installed, remove `node_modules` and run `npm install` again.

- Application crashes on start:
  - Inspect server logs printed to console.
  - Run `node server.js` manually to see the stack trace.
