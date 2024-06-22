# Golang Need to Know

## Introduction

**Configuration**: Configuration files or settings help manage different environments and sensitive information like database credentials, API keys, etc. A common practice is to use environment variables and configuration files (e.g., `.env `files) managed through libraries like `godotenv`.

- **Purpose**: Manage and access environment-specific settings and sensitive information.
- **Example**: Database connection strings, API keys, port numbers.

**Controllers**: Controllers handle incoming HTTP requests, process them, and return responses. They typically interact with services and models to retrieve or manipulate data.

- **Purpose**: Handle HTTP requests and map them to service functions.
- **Example**: User registration, login, profile management.

**Middleware**: Middleware functions are used to process requests before they reach the controllers. Common use cases include authentication, logging, and CORS handling.

- **Purpose**: Intercept and process HTTP requests before they reach the controllers.
- **Example**: JWT authentication, request logging, error handling.

**Models**: Models represent the data structure of your application and interact with the database. They are typically defined using ORM libraries like GORM.

- **Purpose**: Define the schema for your data and provide methods to interact with the database.
- **Example**: User, Product, Order.

**Routes**: Routes define the endpoints of your application and map them to corresponding controller functions.

- **Purpose**: Define the URL endpoints and map them to controller functions.
- **Example**: /auth/register, /auth/login, /profile.

## Summary
- **Configuration**: Manages environment-specific settings and sensitive information.
- **Controller**: Handles HTTP requests and maps them to service functions.
- **Middleware**: Intercepts and processes HTTP requests before they reach controllers.
- **Model**: Defines the data structure and interacts with the database.
- **Route**: Defines the URL endpoints and maps them to controller functions.


Together, these components form a well-structured Go web application using the Gin framework, providing a clear separation of concerns and organized codebase.