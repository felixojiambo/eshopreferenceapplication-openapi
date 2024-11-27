eShop Solution

Overview

The eShop project is a modular e-commerce platform designed to demonstrate a modern microservices architecture. It includes a suite of backend services, client applications, and shared libraries, all managed within a .NET solution.

Solution Structure

The project is organized as follows:

1. Backend Services

Identity Service: Manages user authentication and authorization.

Catalog Service: Handles product listing and search functionality.

Basket Service: Provides shopping cart management.

Order Service: Processes orders and manages the order lifecycle.

Payment Service: Handles payment processing.

Webhook Service: Integrates with external systems for notifications.

2. Client Applications

Mobile BFF: Backend for frontend that aggregates data for mobile apps.

Web App: Blazor WebAssembly project for the e-commerce frontend.

3. Shared Libraries

Event Bus: Implements an event-driven architecture using RabbitMQ.

Observability: Provides centralized logging and metrics.

Prerequisites

.NET 6 or later

Docker (for containerization)

RabbitMQ (message broker)

PostgreSQL (database)

Redis (for caching)

Prometheus and Grafana (for observability)

Git (for version control)

Setup Instructions

Step 1: Clone the Repository

git clone (https://github.com/felixojiambo/eshopreferenceapplication-openapi)

cd eshopreferenceapplication-openapi

Step 2: Build the Solution

dotnet build eShop.sln

Step 3: Run Services Locally

Use Docker Compose for local development:

docker-compose up

Step 4: Run Tests

Unit tests can be executed with the following command:

dotnet test

Development Guide

1. Adding a New Service

Create a new Web API project:

dotnet new webapi -n NewService -o services/new-service

Add it to the solution:

dotnet sln eShop.sln add services/new-service/NewService.csproj

Commit the changes:

git add .
git commit -m "Add NewService to the solution"

2. API Documentation

Swagger is enabled by default for all services. Access it at /swagger on each service's base URL.

3. Event-Driven Communication

Use RabbitMQ to publish and subscribe to domain events.

Add new events to the Event Bus shared library.

Deployment

1. Containerization

Each service includes a Dockerfile.

Build and run containers individually or with Docker Compose.

docker-compose build
docker-compose up -d

2. CI/CD Pipeline

Configure Azure DevOps or GitHub Actions for continuous integration and deployment.

Example CI/CD tasks include:

Building and testing the solution.

Pushing Docker images to a registry.

Deploying services to Kubernetes.

Observability

Logging: Centralized using Serilog and Elasticsearch.

Metrics: Monitored via Prometheus and visualized in Grafana.

Tracing: Distributed tracing enabled with OpenTelemetry.

Contribution Guidelines

Follow coding standards and best practices (e.g., SOLID principles).

Write unit and integration tests for all new features.

Document APIs and modules in the code and README files.

Use meaningful commit messages.

License

This project is licensed under the MIT License. See LICENSE for more details.

Acknowledgments

Special thanks to all contributors and the open-source community for supporting the tools and frameworks used in this project.

