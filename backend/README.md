# Expense Tracker Backend

Spring Boot REST API for the Expense Tracker application.

## Requirements

- Java 17 or later
- MySQL 8 or later
- Maven, or the included Maven wrapper

## Configuration

Update `src/main/resources/application.yml` with your MySQL credentials. The API uses the `expense_tracker` database and runs with the `/api` context path.

## Run the API

```bash
bash mvnw spring-boot:run
```

The backend is available at `http://localhost:8080/api`.

## Main Endpoints

- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/expenses`
- `POST /api/expenses`
- `PUT /api/expenses/{id}`
- `DELETE /api/expenses/{id}`
- `GET /api/expenses/byDate`
- `GET /api/expenses/byDateBetween`
- `GET /api/expenses/byCategory`
- `GET /api/expenses/byCategoryAndDateRange`

Expense endpoints require a valid JWT bearer token.
