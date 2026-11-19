# NoteNest — Cohort 10 (MERN)

Cohort 10 — MERN (NodeJS+ReactJS) assignment for Muhammad Moeen

A full-stack notes application with user authentication, built module by module.

## Tech Stack

| Layer    | Technology                                      |
| -------- | ----------------------------------------------- |
| Backend  | Node.js (ES Modules), Express                   |
| Database | MongoDB Atlas (Mongoose ODM)                    |
| Logging  | Pino (+ pino-http for request logging)          |
| Auth     | JWT, bcrypt password hashing                    |
| Frontend | React (Vite), React Router, Axios               |
| Tests    | Mocha/Chai (backend), Jest (frontend) — later module |

## Modules

| Module | Scope                                                             | Status |
| ------ | ----------------------------------------------------------------- | ------ |
| 1      | Project setup, user authentication (sign up / log in / log out)   | Done   |
| 2      | Notes CRUD APIs + dashboard                                       | Planned |
| 3      | Rich text editor, search/filter, export/import                    | Planned |
| 4      | Unit tests (Mocha/Chai, Jest)                                     | Planned |
| 5      | SonarQube integration                                             | Planned |

## Getting Started

### Prerequisites

- Node.js 18+
- A MongoDB Atlas cluster (free M0 tier works)

### 1. MongoDB Atlas

1. Create a cluster on [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).
2. Under **Database Access**, create a database user.
3. Under **Network Access**, allow your IP (or `0.0.0.0/0` for testing).
4. Copy the connection string: **Connect → Drivers** → `mongodb+srv://<user>:<password>@<cluster>.mongodb.net/`

No schema setup is needed — Mongoose creates the `users` collection on first insert.

### 2. Backend

```bash
cd backend
cp .env.example .env        # paste your Atlas URI into MONGODB_URI, set JWT_SECRET
npm install
npm run dev
```

The API starts on http://localhost:5000 (`GET /health` to verify).

### 3. Frontend

```bash
cd frontend
npm install
npm run dev
```

The app starts on http://localhost:3000 and proxies `/api` requests to the backend.

## API Endpoints

| Method | Endpoint            | Auth    | Description                          |
| ------ | ------------------- | ------- | ------------------------------------ |
| POST   | `/api/auth/register` | —      | Create an account, returns JWT       |
| POST   | `/api/auth/login`    | —      | Sign in, returns JWT                 |
| GET    | `/api/auth/me`       | Bearer | Current user for session restore     |

## Project Structure

```
backend/
  src/
    config/        # env config + mongoose connection
    models/        # mongoose schemas
    controllers/   # request handlers
    services/      # business logic / data access
    routes/        # route definitions
    middleware/    # auth, validation, error handling
    validations/   # zod request schemas
    utils/         # logger, ApiError, jwt helpers
frontend/
  src/
    api/           # axios instance with auth header
    components/    # FormField, ProtectedRoute
    context/       # AuthContext (login/register/logout/session)
    pages/         # Login, Register, Home
    styles/        # global CSS
```
