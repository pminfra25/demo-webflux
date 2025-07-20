# Spring Boot WebFlux Demo

A complete reactive user management system built with Spring Boot WebFlux, demonstrating modern reactive programming patterns and comprehensive testing practices.

## 🌟 Features

- **Reactive Programming**: Built with Spring WebFlux using Mono and Flux
- **Complete CRUD Operations**: Create, Read, Update, Delete users
- **Advanced Search**: Search users by name with partial matching
- **Email Uniqueness**: Validation to prevent duplicate email addresses
- **Immutable Design**: Thread-safe User model with builder-style updates
- **Comprehensive Testing**: 50+ unit and integration tests
- **RESTful API**: Clean REST endpoints with proper HTTP status codes
- **Sample Data**: Pre-loaded test data for quick demonstration
- **🔍 Comprehensive Audit Logging**: Structured logging for all business operations
- **📊 Performance Monitoring**: Method execution timing and performance metrics
- **🔒 Security Auditing**: Track all user operations with detailed context
- **📋 Swagger Documentation**: Interactive API documentation with OpenAPI 3.0

## 🏗️ Architecture

```
├── Model Layer (User.java)
├── Repository Layer (UserRepository.java, InMemoryUserRepository.java)
├── Service Layer (UserService.java)
├── Controller Layer (UserController.java)
└── Configuration (ApplicationConfig.java)
```

## 🚀 Quick Start

### Prerequisites

- Java 17 or higher
- Maven 3.6 or higher

### Running the Application

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd demo-webflux
   ```

2. **Run the application**
   ```bash
   ./mvnw spring-boot:run
   ```

3. **Access the API**
   - Base URL: `http://localhost:8080`
   - API endpoints: `http://localhost:8080/api/users`

## 📋 API Endpoints

### User Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET    | `/api/users` | Get all users |
| GET    | `/api/users/{id}` | Get user by ID |
| GET    | `/api/users/email/{email}` | Get user by email |
| GET    | `/api/users/search?name={term}` | Search users by name |
| POST   | `/api/users` | Create new user |
| PUT    | `/api/users/{id}` | Update user |
| DELETE | `/api/users/{id}` | Delete user |
| GET    | `/api/users/count` | Get total user count |
| GET    | `/api/users/{id}/exists` | Check if user exists |

### Sample API Calls

**Get all users:**
```bash
curl http://localhost:8080/api/users
```

**Create a new user:**
```bash
curl -X POST http://localhost:8080/api/users \
  -H "Content-Type: application/json" \
  -d '{
    "firstName": "John",
    "lastName": "Doe",
    "email": "john.doe@example.com"
  }'
```

**Search users by name:**
```bash
curl "http://localhost:8080/api/users/search?name=john"
```

## 🧪 Testing

The project includes comprehensive test coverage across all layers:

### Running Tests

```bash
# Run all tests
./mvnw test

# Run specific test class
./mvnw test -Dtest=UserTest

# Run with coverage
./mvnw test jacoco:report
```

### Test Categories

- **Unit Tests**: Model, Repository, Service, Controller layers
- **Integration Tests**: End-to-end API testing
- **Reactive Testing**: Using StepVerifier for reactive streams
- **Mock Testing**: Isolated testing with Mockito

## 📦 Sample Data

The application comes pre-loaded with sample users:

1. **John Doe** - john.doe@example.com
2. **Jane Smith** - jane.smith@example.com
3. **Alice Johnson** - alice.johnson@example.com
4. **Bob Brown** - bob.brown@example.com

## 🛠️ Technology Stack

- **Framework**: Spring Boot 3.x
- **Reactive**: Spring WebFlux
- **Build Tool**: Maven
- **Testing**: JUnit 5, Mockito, Spring Boot Test
- **Reactive Testing**: StepVerifier (Project Reactor)
- **Documentation**: Comprehensive Javadoc

## 📋 Audit Logging & Monitoring

The application includes comprehensive audit logging and performance monitoring capabilities:

### 🔍 Audit Logging Features

- **Structured Logging**: All operations logged in a consistent, parseable format
- **Business Operations**: Create, Read, Update, Delete, Search operations tracked
- **Security Events**: Failed login attempts, duplicate email detection, invalid operations
- **Performance Metrics**: Method execution times and reactive stream performance
- **Error Tracking**: Detailed error context and stack traces
- **Method Tracing**: Entry/exit logging for debugging and performance analysis

### 📊 Log Format

```
[AUDIT] [TIMESTAMP] [OPERATION] [USER_ID] [DETAILS] [STATUS]
```

**Example Audit Logs:**
```
[AUDIT] [2023-12-01 10:30:15.123] [CREATE_USER] [123e4567-e89b-12d3-a456-426614174000] [User created: John Doe (john.doe@example.com)] [SUCCESS]
[AUDIT] [2023-12-01 10:31:22.456] [READ_USER] [123e4567-e89b-12d3-a456-426614174000] [User retrieved using method: BY_ID] [SUCCESS]
[AUDIT] [2023-12-01 10:32:05.789] [CREATE_USER] [N/A] [User creation failed for email: duplicate@example.com - Reason: Email already exists] [FAILED]
```

### ⚡ Performance Monitoring

- **Reactive Stream Timing**: Accurate timing for Mono and Flux operations
- **HTTP Request Tracking**: Complete request/response cycle monitoring
- **Method Performance**: Individual method execution time tracking
- **Resource Usage**: Memory and processing time metrics

### 🔧 Logging Configuration

Configure logging levels in `application.properties`:

```properties
# Audit logging level
logging.level.com.example.demo.logging.AuditLogger=INFO

# Performance monitoring
logging.level.com.example.demo.logging.PerformanceLoggingAspect=DEBUG

# File logging for audit trail
logging.file.name=logs/demo-webflux.log
logging.file.max-size=10MB
logging.file.max-history=30
```

### 📝 Sample Audit Events

| Operation | Logged Events |
|-----------|---------------|
| **User Creation** | Method entry, validation checks, success/failure, method exit |
| **User Retrieval** | Method entry, database query, found/not found, method exit |
| **User Update** | Method entry, validation, changes tracked, success/failure, method exit |
| **User Deletion** | Method entry, existence check, deletion result, method exit |
| **Search Operations** | Method entry, search terms, result count, method exit |

## 🏛️ Project Structure

```
src/
├── main/
│   ├── java/com/example/demo/
│   │   ├── DemoWebfluxApplication.java
│   │   ├── config/
│   │   │   ├── ApplicationConfig.java
│   │   │   └── SwaggerConfig.java
│   │   ├── controller/UserController.java
│   │   ├── logging/
│   │   │   ├── AuditLogger.java
│   │   │   └── PerformanceLoggingAspect.java
│   │   ├── model/User.java
│   │   ├── repository/
│   │   │   ├── UserRepository.java
│   │   │   └── impl/InMemoryUserRepository.java
│   │   └── service/UserService.java
│   └── resources/application.properties
└── test/
    └── java/com/example/demo/
        ├── DemoWebfluxApplicationIntegrationTest.java
        ├── DemoWebfluxApplicationTests.java
        ├── controller/UserControllerTest.java
        ├── logging/AuditLoggerTest.java
        ├── model/UserTest.java
        ├── repository/impl/InMemoryUserRepositoryTest.java
        └── service/UserServiceTest.java
```

## 🔧 Configuration

### Application Properties

The application runs on port 8080 by default. To change the port:

```properties
server.port=8081
```

### Development Mode

For development, the application includes:
- Automatic sample data loading
- CORS enabled for frontend development
- DevTools for hot reloading

## 🎯 Key Design Patterns

1. **Repository Pattern**: Clean separation of data access logic
2. **Service Layer Pattern**: Business logic encapsulation
3. **Immutable Objects**: Thread-safe User model
4. **Reactive Programming**: Non-blocking I/O operations
5. **Dependency Injection**: Spring's IoC container

## 📈 Performance Characteristics

- **Non-blocking I/O**: Handles thousands of concurrent requests
- **Memory Efficient**: Reactive streams with backpressure
- **Thread-safe**: Concurrent operations support
- **Fast Startup**: Optimized Spring Boot configuration

## 🔮 Future Enhancements

- [ ] Database integration (R2DBC/MongoDB Reactive)
- [ ] User authentication and authorization
- [ ] Pagination and sorting
- [ ] Validation framework integration
- [ ] OpenAPI/Swagger documentation
- [ ] Metrics and monitoring
- [ ] Docker containerization

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👨‍💻 Author

**GitHub Copilot** - *AI Assistant*

---

*Built with ❤️ using Spring Boot WebFlux and reactive programming principles*
