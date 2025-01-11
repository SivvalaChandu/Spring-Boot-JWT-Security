# :closed_lock_with_key: Spring Boot JWT Authentication and Authorization :lock:

This project demonstrates a basic implementation of JWT-based authentication and authorization in a Spring Boot application. It includes functionalities like user registration, login, and role-based access control for various endpoints using JWT tokens.

## Prerequisites

Before running the project, ensure you have the following installed:

- **Java 11 or later** - To run Spring Boot applications
- **Maven** or **Gradle** - To build the project
- **PostgreSQL** (or any other database) for persistent data storage (or use an in-memory database for simplicity)

## Project Structure

- `com.Backend.JWTImp.config`: Contains security-related configurations, including `SecurityConfig` for JWT authentication.
- `com.Backend.JWTImp.controller`: Handles HTTP requests, including the `AuthController` for login and registration, and the `UserController` for user management.
- `com.Backend.JWTImp.dto`: Contains data transfer objects (DTOs) like `LoginDto` and `AuthResponseDto`.
- `com.Backend.JWTImp.jwt`: Contains JWT utilities (`JwtUtils`) and the JWT filter (`JwtAuthenticationFilter`).
- `com.Backend.JWTImp.model`: Contains `User` and `Role` entities.
- `com.Backend.JWTImp.repository`: Includes JPA repositories for interacting with the database.
- `com.Backend.JWTImp.service`: Implements business logic for user authentication, registration, and management.

## Features

- **JWT Authentication**: Secure the endpoints with JWT token-based authentication.
- **Role-Based Authorization**: Allow different access levels to various endpoints based on roles.
- **Login & Registration**: Register a new user and log in to get a JWT token.

## Installation
 **Clone the repository**:
   ```
   git clone https://github.com/SivvalaChandu/Spring-Boot-JWT-Security.git
   cd Spring-Boot-JWT-Security
  ```

## API Endpoints

### 1. **POST /api/auth/register**
   - Registers a new user.
   - **Request Body**:
     ```json
     {
       "id": "user-id",
       "username": "your-username",
       "email": "your-email@example.com",
       "password": "your-password"
     }
     ```

   - **Response**: 
     A JWT token will be returned in the response header:
     ```http
     Authorization: Bearer <JWT_TOKEN>
     ```

### 2. **POST /api/auth/login**
   - Logs in with username and password.
   - **Request Body**:
     ```json
     {
       "username": "your-username",
       "password": "your-password"
     }
     ```

   - **Response**: 
     A JWT token will be returned in the response header:
     ```http
     Authorization: Bearer <JWT_TOKEN>
     ```

### 3. **GET /api/users/**
   - Fetches all users (Requires `ROLE_USER`).
   - **Authorization**: Bearer `<JWT_TOKEN>`

### 4. **GET /api/users/{id}**
   - Fetches user by ID (Requires `ROLE_USER`).
   - **Authorization**: Bearer `<JWT_TOKEN>`

### 5. **PUT /api/users/{id}**
   - Updates the user by ID (Requires `ROLE_USER`).
   - **Request Body**:
     ```json
     {
       "username": "updated-username",
       "email": "updated-email@example.com",
       "password": "updated-password"
     }
     ```
   - **Authorization**: Bearer `<JWT_TOKEN>`

### 6. **DELETE /api/users/{id}**
   - Deletes the user by ID (Requires `ROLE_USER`).
   - **Authorization**: Bearer `<JWT_TOKEN>`


### Security

   - **JWT Token Expiry**: JWT tokens expire after 10 minutes by default.
   - **Role-Based Authorization**: The ROLE_USER role is required to access certain endpoints.
   - **Stateless Session Management**: The app does not store sessions on the server; each request is validated with the JWT token.
