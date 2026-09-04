# Expense Tracker Backend

Spring Boot REST API for the Expense Tracker application.

## Requirements

- Java 17 or later
- MySQL 8 or later
- Maven, or the included Maven wrapper

## Configuration

Configure the environment variables in `.env.example` in your shell or deployment provider. The API uses the `expense_tracker` database and runs with the `/api` context path. Never commit production database credentials or `JWT_SECRET`.

## Run the API

```bash
bash mvnw spring-boot:run
```

The backend is available at `http://localhost:8080/api`.

## Deploy with Render

1. Create a new GitHub repository containing the contents of this directory.
2. Create a Render **Web Service** from that repository and choose Docker, or use the included `render.yaml`.
3. Set `DB_URL`, `DB_USERNAME`, `DB_PASSWORD`, and `FRONTEND_URL` in Render. `JWT_SECRET` must be a long random value.
4. Use a managed MySQL database and set `DB_URL` to its JDBC connection URL.

Render supplies the `PORT` variable automatically. The frontend must use the resulting service URL with `/api` appended.

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
