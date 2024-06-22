# Node Js Need to Know

## Introduction

**Configuration**: Configuration files manage environment-specific settings and sensitive information like database credentials, API keys, etc. A common practice is to use environment variables and configuration files (e.g., .env files) managed through libraries like dotenv.

**Controllers**: Controllers handle incoming HTTP requests and return responses to the client. They typically interact with services and models to retrieve or manipulate data.

**Middleware**: Middleware functions are used to process requests before they reach the controllers. Common use cases include authentication, logging, and CORS handling.

**Models**: Models represent the data structure of your application and interact with the database. They are typically defined using ORM libraries like Mongoose for MongoDB.

**Routes**: Routes define the endpoints of your application and map them to corresponding controller functions.

**Main Application File (app.js)**:
The main application file sets up the Express app, connects to the database, and configures middleware and routes.

**Nodemon**: Nodemon is a tool that helps develop Node.js applications by automatically restarting the application when file changes are detected. The nodemon.json file is used to configure Nodemon.

## Summary
- **Configuration**: Manages environment-specific settings and sensitive information.
- **Controller**: Handles HTTP requests and maps them to service functions.
- **Middleware**: Intercepts and processes HTTP requests before they reach controllers.
- **Model**: Defines the data structure and interacts with the database.
- **Route**: Defines the URL endpoints and maps them to controller functions.
- **Main Application File (app.js)**: Sets up the Express app, connects to the database, and configures middleware and routes.
- **Nodemon Configuration (nodemon.json)**: Configures Nodemon to watch for file changes and restart the application automatically.

Together, these components form a well-structured Node.js application, providing a clear separation of concerns and organized codebase.


