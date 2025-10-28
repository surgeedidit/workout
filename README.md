# Workout Tracking API

A production-ready RESTful API for tracking workouts, built with Go and PostgreSQL. This project was developed following best practices from the [Complete Go course](https://frontendmasters.com/courses/complete-go/) on Frontend Masters, with custom implementations and enhancements.

## Features

- **User Authentication** - Token-based authentication with OAuth 2.0
- **Workout Management** - Create, read, update, and delete workout records
- **Workout Entries** - Track individual exercise entries within workouts
- **Database Migrations** - Version-controlled schema changes with Goose
- **Comprehensive Testing** - Unit tests for core functionality
- **Dockerized Setup** - Easy deployment with Docker Compose
- **Middleware Support** - Authentication and logging middleware
- **JSON API** - RESTful endpoints with proper error handling

## Tech Stack

- **Go** 1.24.2+ - Backend language
- **PostgreSQL** - Primary database
- **Docker & Docker Compose** - Containerization
- **Goose** - Database migration tool

## Project Structure
```
.
├── internal/
│   ├── api/          # HTTP handlers
│   ├── app/          # Application setup
│   ├── middleware/   # Custom middleware
│   ├── routes/       # Route definitions
│   ├── store/        # Database layer
│   ├── tokens/       # Token generation & validation
│   └── utils/        # Helper functions
├── migrations/       # SQL migration files
├── docker-compose.yml
└── main.go
```

## Getting Started

### Prerequisites

- [Go](https://go.dev/doc/install) (version 1.24.2 or higher)
- [Docker and Docker Compose](https://www.docker.com/)
- [Goose](https://github.com/pressly/goose) for migrations

### Installation

1. Clone the repository
```bash
git clone https://github.com/surgeedidit/workout.git
cd workout
```

2. Start the PostgreSQL container
```bash
docker-compose up -d
```

3. Run database migrations
```bash
goose -dir migrations postgres "user=postgres password=postgres dbname=workouts sslmode=disable" up
```

4. Start the API server
```bash
go run main.go
```

The API will be available at `http://localhost:8080`

## Configuration

Database connection settings can be modified in `docker-compose.yml`:
```yaml
ports:
  - "5432:5432"  # Change to "5433:5432" if port 5432 is in use
```

If you encounter a "command not found" error with Goose, add Go binaries to your PATH:
```bash
export PATH=$HOME/go/bin:$PATH
```

For a permanent fix, add this to your `.zshrc` or `.bashrc`.

## API Endpoints

### Authentication
- `POST /api/v1/auth/register` - Register new user
- `POST /api/v1/auth/login` - User login
- `POST /api/v1/auth/token` - Generate access token

### Workouts
- `GET /api/v1/workouts` - List all workouts
- `GET /api/v1/workouts/:id` - Get workout by ID
- `POST /api/v1/workouts` - Create new workout
- `PUT /api/v1/workouts/:id` - Update workout
- `DELETE /api/v1/workouts/:id` - Delete workout

## Running Tests
```bash
go test ./internal/store/...
```

## Development Notes

This project was built following the Complete Go course structure with additional customizations and real-world production considerations. The implementation includes proper error handling, authentication middleware, and a clean separation of concerns.

## Acknowledgments

Built with guidance from the [Complete Go](https://frontendmasters.com/courses/complete-go/) course by Frontend Masters. Course materials provided the foundation, with custom implementations and extensions added throughout development.

## License

MIT