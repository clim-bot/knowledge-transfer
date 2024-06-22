# Nest JS Need to Know

## Introduction

`auth.controller.ts`
**Controller**: Controllers are responsible for handling incoming HTTP requests and returning responses to the client. In the context of authentication, the controller will have endpoints for user registration, login, account activation, password reset, etc.

- **Purpose**: Handle HTTP requests and map them to corresponding service methods.
- **Example**: Registering a user, logging in a user, activating an account, etc.

`auth.service.ts`
**Service**: Services contain the business logic of the application. They are responsible for data processing and interaction with the database. In authentication, services handle user creation, validation, token generation, etc.

- **Purpose**: Encapsulate the business logic and data manipulation.
- **Example**: Hashing passwords, generating JWT tokens, sending emails.

`auth.module.ts`
**Module**: Modules are used to organize the application structure by grouping related components like controllers and services. A module in NestJS is a class annotated with a @Module decorator.

- **Purpose**: Define the scope for the components it manages and provide dependency injection.
- **Example**: Grouping the authentication-related controllers, services, and providers.

`jwt-auth.guard.ts`
**Guard**: Guards are used to control the flow of request handling and provide authorization. They implement logic to determine whether a request should proceed or not.

- **Purpose**: Implement authorization logic to protect routes.
- **Example**: Checking if a user has a valid JWT token before allowing access to certain routes.

`jwt.strategy.ts`
**Strategy**: Strategies are part of the authentication process. In NestJS, strategies are used with Passport to implement different types of authentication methods, such as JWT, OAuth, etc.

- **Purpose**: Define how the authentication process should be carried out.
- **Example**: Extracting and validating the JWT token from requests.

## Summary

- **Controller** : Handles HTTP requests and responses, mapping them to service methods.
- **Service**: Contains business logic and interacts with the database or other services.
- **Module**: Organizes related components, such as controllers and services, and provides dependency injection.
- **Guard**: Controls request flow and implements authorization logic.
- **Strategy**: Defines the authentication process, such as extracting and validating JWT tokens.

These components together form the backbone of the authentication system in your NestJS application.