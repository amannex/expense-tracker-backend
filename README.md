# Expense Tracker Backend

Spring Boot REST API for the Expense Tracker application. The frontend is maintained separately in the [`expense-tracker-frontend`](https://github.com/amannex/expense-tracker-frontend) repository.

## Backend features

- JWT-based registration and login
- BCrypt password hashing
- Protected user-specific expense endpoints
- Create, read, update, and delete expenses
- Expense filtering by date, date range, and category
- MySQL persistence with Spring Data JPA
- Configurable CORS for the deployed frontend
- Public `/api/health` endpoint
- Docker and Render deployment support

## Technology stack

- Java 17
- Spring Boot 3
- Spring Security
- Spring Data JPA and Hibernate
- MySQL
- Maven
- JSON Web Tokens

## Quick start

Requirements:

- Java 17 or later
- MySQL 8 or later

Configure the database and JWT variables from [`backend/.env.example`](backend/.env.example), then start the API:

```bash
cd backend
./mvnw spring-boot:run
```

The API is available at:

```text
http://localhost:8080/api
```

Health check:

```bash
curl http://localhost:8080/api/health
```

## Documentation

For complete configuration, API endpoint, Docker, Render deployment, and project structure details, see [`backend/README.md`](backend/README.md).

## Related repository

Frontend: https://github.com/amannex/expense-tracker-frontend
