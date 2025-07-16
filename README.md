# Go CRUD API

A simple and efficient CRUD (Create, Read, Update, Delete) REST API built with Go and PostgreSQL.

## Features

- Full CRUD operations for user management
- PostgreSQL database integration
- Environment-based configuration
- JSON API responses
- Proper error handling
- RESTful endpoints

## Tech Stack

- **Language**: Go 1.21+
- **Database**: PostgreSQL
- **Router**: Gorilla Mux
- **Environment**: godotenv

## Project Structure

```
.
├── main.go          # Application entry point and routing
├── handlers.go      # HTTP request handlers
├── models.go        # Data models and structs
├── database.go      # Database connection and setup
├── .env            # Environment variables
├── go.mod          # Go module dependencies
└── README.md       # This file
```

## Installation

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd crud-api
   ```

2. **Install dependencies**

   ```bash
   go mod tidy
   ```

3. **Set up PostgreSQL database**

   - Install PostgreSQL on your system
   - Create a database for the application

4. **Configure environment variables**

   Update the `.env` file with your database credentials:

   ```env
   DB_CONNECTION=pgsql
   DB_HOST=localhost
   DB_PORT=5432
   DB_DATABASE=crud_db
   DB_USERNAME=postgres
   DB_PASSWORD=your_password
   ```

5. **Run the application**
   ```bash
   go run .
   ```

The server will start on `http://localhost:8080`

## API Endpoints

### Users

| Method | Endpoint      | Description          | Request Body                            |
| ------ | ------------- | -------------------- | --------------------------------------- |
| GET    | `/users`      | Get all users        | -                                       |
| GET    | `/users/{id}` | Get user by ID       | -                                       |
| POST   | `/users`      | Create new user      | `{"name": "string", "email": "string"}` |
| PUT    | `/users/{id}` | Update existing user | `{"name": "string", "email": "string"}` |
| DELETE | `/users/{id}` | Delete user          | -                                       |

## API Usage Examples

### Create a new user

```bash
curl -X POST http://localhost:8080/users \
  -H "Content-Type: application/json" \
  -d '{"name":"John Doe","email":"john@example.com"}'
```

### Get all users

```bash
curl http://localhost:8080/users
```

### Get a specific user

```bash
curl http://localhost:8080/users/1
```

### Update a user

```bash
curl -X PUT http://localhost:8080/users/1 \
  -H "Content-Type: application/json" \
  -d '{"name":"Jane Doe","email":"jane@example.com"}'
```

### Delete a user

```bash
curl -X DELETE http://localhost:8080/users/1
```

## Response Format

### Success Response

```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "created_at": "2024-01-01T12:00:00Z",
  "updated_at": "2024-01-01T12:00:00Z"
}
```

### Error Response

```json
{
  "error": "Error message description"
}
```

## HTTP Status Codes

- `200 OK` - Successful GET, PUT requests
- `201 Created` - Successful POST request
- `204 No Content` - Successful DELETE request
- `400 Bad Request` - Invalid request data
- `404 Not Found` - Resource not found
- `500 Internal Server Error` - Server error

## Database Schema

### Users Table

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Environment Variables

| Variable      | Description       | Default   |
| ------------- | ----------------- | --------- |
| DB_CONNECTION | Database type     | pgsql     |
| DB_HOST       | Database host     | localhost |
| DB_PORT       | Database port     | 5432      |
| DB_DATABASE   | Database name     | crud_db   |
| DB_USERNAME   | Database username | postgres  |
| DB_PASSWORD   | Database password | (empty)   |

## Development

### Running Tests

```bash
go test ./...
```

### Building for Production

```bash
go build -o crud-api
./crud-api
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

If you encounter any issues or have questions, please open an issue on the repository.
