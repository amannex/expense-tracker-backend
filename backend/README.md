# Expense Tracker Backend

Spring Boot REST API for secure personal expense management. This service provides authentication, JWT authorization, expense management, filtering, and MySQL persistence for the separate `expense-tracker-frontend` application.

## Features

- User registration and login
- JWT-based authentication
- BCrypt password hashing
- Protected, user-specific expense endpoints
- Create, read, update, and delete expenses
- Filter expenses by date, date range, category, and category/date range
- MySQL persistence with Spring Data JPA and Hibernate
- Configurable CORS for the deployed frontend
- Health-check endpoint
- Docker and Render deployment support
- Environment-based configuration for production secrets

## Tech stack

- Java 17
- Spring Boot 3
- Spring Security
- Spring Data JPA
- Hibernate
- MySQL
- Maven
- JSON Web Tokens
- Docker

## Requirements

- Java 17 or later
- MySQL 8 or later
- Maven, or the included Maven wrapper

## Configuration

Copy `.env.example` values into your local shell or configure them in your hosting provider. Spring Boot reads these variables automatically.

```env
DB_URL=jdbc:mysql://localhost:3306/expense_tracker?createDatabaseIfNotExist=true&useSSL=false&serverTimezone=UTC
DB_USERNAME=root
DB_PASSWORD=your-password
JWT_SECRET=replace-with-a-long-random-secret
JWT_EXPIRATION=86400000
FRONTEND_URL=http://localhost:5173
PORT=8080
```

`FRONTEND_URL` may contain a comma-separated list of allowed frontend origins. Never commit production database credentials or `JWT_SECRET`.

## Run locally

Start MySQL, configure the environment variables, and run:

```bash
bash mvnw spring-boot:run
```

The API runs at:

```text
http://localhost:8080/api
```

## API endpoints

### Authentication

```text
POST /api/auth/register
POST /api/auth/login
```

Authentication endpoints return a JWT token. Send it on protected requests:

```text
Authorization: Bearer <token>
```

### Expenses

```text
GET    /api/expenses
GET    /api/expenses/{id}
POST   /api/expenses
PUT    /api/expenses/{id}
DELETE /api/expenses/{id}
```

### Expense filters

```text
GET /api/expenses/byDate?date=YYYY-MM-DD
GET /api/expenses/byDateBetween?startDate=YYYY-MM-DD&endDate=YYYY-MM-DD
GET /api/expenses/byCategory?Category=<category>&date=YYYY-MM-DD
GET /api/expenses/byCategoryAndDateRange?Category=<category>&startdate=YYYY-MM-DD&endDate=YYYY-MM-DD
```

All expense endpoints require a valid JWT bearer token and return data for the authenticated user.

### Health check

```text
GET /api/health
```

Returns:

```json
{
  "status": "ok"
}
```

## Docker

Build the image from the backend directory:

```bash
docker build -t expense-tracker-backend .
```

Run it with your database and frontend configuration:

```bash
docker run --rm -p 8080:8080 \
  -e DB_URL="jdbc:mysql://your-host:3306/expense_tracker" \
  -e DB_USERNAME="your-database-user" \
  -e DB_PASSWORD="your-database-password" \
  -e JWT_SECRET="your-long-random-secret" \
  -e FRONTEND_URL="https://your-frontend-url.example.com" \
  expense-tracker-backend
```

## Deploy with Render

The repository includes `render.yaml` and a production `Dockerfile`.

1. Create a Render **Web Service** from the backend GitHub repository.
2. Select Docker as the runtime, or use the included Blueprint configuration.
3. Connect a managed MySQL database.
4. Configure `DB_URL`, `DB_USERNAME`, `DB_PASSWORD`, and `FRONTEND_URL`.
5. Set `JWT_SECRET` to a long, randomly generated secret. Render can generate it automatically through `render.yaml`.
6. Use the deployed service URL followed by `/api` as the frontend's `VITE_API_URL`.

Render provides the `PORT` environment variable automatically.

## Project structure

```text
backend/
├── src/main/java/com/expensetracker/
│   ├── config/
│   ├── controller/
│   ├── dto/
│   ├── exception/
│   ├── model/
│   ├── repository/
│   ├── security/
│   └── service/
├── src/main/resources/application.yml
├── Dockerfile
├── render.yaml
└── pom.xml
```

## Related repository

Frontend application:

https://github.com/amannex/expense-tracker-frontend
