# Spring Boot Basic Authentication Lab

A Spring Security lab project from a Spring Boot Udemy course demonstrating **HTTP Basic Authentication**, authorization, and role-based access control in a REST API.

## Project Overview

This project implements a **Contact Management API** with Spring Security features focused on **HTTP Basic Authentication**:
- **HTTP Basic Authentication** (Primary Focus)
- Role-based Access Control (RBAC)
- Method-level security using `@PreAuthorize`
- In-memory user authentication
- Stateless session management
- CSRF protection configuration

## Technology Stack

- **Java Version**: 21
- **Spring Boot**: 3.5.5
- **Spring Security**: Latest (from spring-boot-starter-security)
- **Build Tool**: Maven
- **API Type**: REST

## Project Structure

```
src/main/java/com/bank/app/
├── AppMainApplication.java      # Spring Boot Application Entry Point
├── SecurityConfig.java          # Spring Security Configuration
└── ContactController.java       # REST API Endpoints

src/main/resources/
└── application.properties       # Application Configuration
```

## Key Components

### 1. SecurityConfig.java
Configures Spring Security with the following features:

#### Authorization Rules:
- **Public Endpoints**: `/contacts/public/**` - Accessible to all users
- **GET /contacts**: Requires `USER` or `ADMIN` role
- **POST /contacts**: Requires `ADMIN` role
- **DELETE /contacts/{id}**: Requires `ADMIN` role

#### Authentication:
- In-memory user authentication with two pre-configured users:
  - **User**: username=`user`, password=`user123`, role=`USER`
  - **Admin**: username=`admin`, password=`admin123`, role=`ADMIN`

#### Security Features:
- Stateless session management (`SessionCreationPolicy.STATELESS`)
- HTTP Basic authentication
- CSRF protection disabled (for API testing)
- Method-level security enabled (`@EnableMethodSecurity`)

### 2. ContactController.java
REST API endpoints demonstrating role-based access:

| Endpoint | Method | Auth Required | Roles | Description |
|----------|--------|---------------|-------|-------------|
| `/contacts` | GET | Yes | USER, ADMIN | Get all contacts |
| `/contacts` | POST | Yes | ADMIN | Add a new contact |
| `/contacts/{id}` | DELETE | Yes | ADMIN | Delete a contact |
| `/contacts/public/info` | GET | No | - | Public information |

## Running the Application

### Prerequisites
- JDK 21 or higher
- Maven 3.6+

### Steps

1. **Clone/Navigate to the project**:
   ```bash
   cd app-security
   ```

2. **Build the project**:
   ```bash
   ./mvnw clean install
   ```

3. **Run the application**:
   ```bash
   ./mvnw spring-boot:run
   ```

The application will start on `http://localhost:8080`

## Testing the API

### Using cURL

#### 1. Access Public Endpoint (No Authentication Required)
```bash
curl http://localhost:8080/contacts/public/info
```

#### 2. Get Contacts (User Role)
```bash
curl -u user:user123 http://localhost:8080/contacts
```

#### 3. Add Contact (Admin Role)
```bash
curl -X POST -u admin:admin123 http://localhost:8080/contacts
```

#### 4. Delete Contact (Admin Role)
```bash
curl -X DELETE -u admin:admin123 http://localhost:8080/contacts/1
```

#### 5. Attempt Unauthorized Access
```bash
# This will fail - USER cannot POST
curl -X POST -u user:user123 http://localhost:8080/contacts
```

### Using Postman

1. Create a new request
2. Set the authentication type to **Basic Auth**
3. Enter username and password
4. Send the request

## Default Credentials

| Username | Password | Role |
|----------|----------|------|
| user | user123 | USER |
| admin | admin123 | ADMIN |

## Learning Objectives

This lab covers:
- ✅ **Setting up HTTP Basic Authentication in Spring Security** (Primary Focus)
- ✅ Configuring HTTP Basic authentication with in-memory user store
- ✅ Implementing authorization rules at the endpoint level
- ✅ Using `@PreAuthorize` for method-level security
- ✅ Managing user roles and authorities
- ✅ Understanding stateless API security
- ✅ Password encoding with BCrypt

## Security Features Demonstrated

1. **Authentication**: Validates user identity using HTTP Basic Auth
2. **Authorization**: Enforces role-based access control on endpoints
3. **Password Encoding**: Uses BCrypt for secure password storage
4. **CSRF Protection**: Configured and can be enabled for forms
5. **Method Security**: Annotation-based access control with `@PreAuthorize`
6. **Stateless Sessions**: RESTful API without session state

## Course Context

This project is part of a Spring Boot full-stack Udemy course, specifically designed as a lab to understand how Spring Security integrates with Spring Boot applications to protect REST APIs.

## Notes

- The application uses in-memory authentication for lab purposes. In production, use a database-backed user service
- CSRF protection is disabled for API testing; enable it in production for web applications
- Default session management is stateless, suitable for RESTful APIs
- Consider using JWT or OAuth2 for more advanced security scenarios in production applications


---

**Course**: Spring Boot Full Stack - Udemy  
**Lab Type**: Security Configuration & Authorization  
**Difficulty**: Beginner to Intermediate
