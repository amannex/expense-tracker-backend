# Expense Tracker

A full-stack personal expense management application with a React and TypeScript frontend and a Spring Boot REST API.

## Features

- JWT-based registration, login, and protected routes
- Create, edit, delete, and browse expenses
- Filter expenses by date, date range, and category
- Dashboard with monthly totals, averages, category breakdown, and recent expenses
- Monthly budget progress indicator
- Multi-currency display with persistent currency selection
- Responsive dashboard layout with Chakra UI
- MySQL persistence with JPA/Hibernate

## Tech Stack

### Frontend

- React 18
- TypeScript
- Vite
- Chakra UI
- React Router
- Axios
- Day.js

### Backend

- Java 17
- Spring Boot 3
- Spring Security
- Spring Data JPA / Hibernate
- MySQL
- Maven
- JWT

## Prerequisites

- Node.js 18 or later
- Java 17 or later
- MySQL 8 or later

## Getting Started

### 1. Clone the repository

```bash
git clone <repository-url>
cd expense-tracker-app
```

### 2. Configure MySQL

Update `backend/src/main/resources/application.yml` with the local MySQL username and password. The application uses the `expense_tracker` database and creates it automatically when supported by the configured MySQL connection.

### 3. Start the backend

```bash
cd backend
bash mvnw spring-boot:run
```

The API runs at `http://localhost:8080/api`.

### 4. Start the frontend

In a separate terminal:

```bash
cd frontend
npm install
npm run dev
```

The frontend runs at `http://localhost:5173`.

## Split into two GitHub repositories

The application is already isolated into two deployable projects:

- `frontend/` - React/Vite static site
- `backend/` - Spring Boot API

To publish them as separate repositories, create two empty GitHub repositories and push each directory independently:

```bash
git subtree split --prefix=frontend -b frontend-repo
git push <frontend-repository-url> frontend-repo:main

git subtree split --prefix=backend -b backend-repo
git push <backend-repository-url> backend-repo:main
```

The frontend is configured for Vercel and the backend for Docker/Render. Configure `VITE_API_URL` in the frontend and the database/JWT/CORS variables documented in `backend/README.md` before deploying.

## Currency Support

The dashboard supports USD, EUR, GBP, INR, CAD, AUD, and JPY. INR is the default for new users. The selected currency is saved locally and updates dashboard totals, budget progress, category breakdowns, and expense tables.

## API Overview

### Authentication

- `POST /api/auth/register` - Register a user
- `POST /api/auth/login` - Log in and receive a JWT

### Expenses

- `GET /api/expenses` - Get the current user's expenses
- `GET /api/expenses/{id}` - Get an expense
- `POST /api/expenses` - Create an expense
- `PUT /api/expenses/{id}` - Update an expense
- `DELETE /api/expenses/{id}` - Delete an expense

### Filtering

- `GET /api/expenses/byDate`
- `GET /api/expenses/byDateBetween`
- `GET /api/expenses/byCategory`
- `GET /api/expenses/byCategoryAndDateRange`

All expense endpoints require a valid bearer token.

## Project Structure

```text
expense-tracker-app/
├── backend/
│   └── src/main/java/com/expensetracker/
└── frontend/
    └── src/
        ├── components/
        ├── context/
        ├── constants/
        ├── pages/
        ├── services/
        └── types/
```

## License

This project is for personal and educational use.
