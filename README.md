# eShop Microservices Architecture

## Table of Contents
- [Introduction](#introduction)
- [Architecture Overview](#architecture-overview)
- [Services](#services)
  - [Identity Service](#identity-service)
  - [Catalog Service](#catalog-service)
  - [Order Service](#order-service)
  - [Basket Service](#basket-service)
  - [Payment Service](#payment-service)
  - [Webhook Service](#webhook-service)
- [Client Applications](#client-applications)
  - [Mobile BFF (Backend for Frontend)](#mobile-bff-backend-for-frontend)
  - [Web App](#web-app)
- [Shared Libraries](#shared-libraries)
  - [Event Bus](#event-bus)
  - [Observability](#observability)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Setup Instructions](#setup-instructions)
- [Project Structure](#project-structure)
- [API Documentation](#api-documentation)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## Introduction

Welcome to the **eShop** project—a scalable and maintainable e-commerce platform built using a **microservices architecture**. This system is designed to handle various aspects of an online store, including user authentication, product management, order processing, shopping cart functionality, payment processing, and more.

---

## Architecture Overview

The eShop system is divided into multiple independent services, each responsible for a specific domain. This modular approach ensures scalability, ease of maintenance, and flexibility in deploying and updating individual components without affecting the entire system.

<img width="612" alt="e" src="https://github.com/user-attachments/assets/d7598dda-cf50-4cc6-9e9c-8ab0af998e0e">

## Services

### 1. Identity Service

**Directory**: `services/identity-service`

**Purpose**: Handles user authentication, authorization, and management. This service manages user registration, login, profile updates, role assignments, and security mechanisms like JWT tokens.

**Key Features**:
- User Registration and Login
- JWT Authentication
- Role-Based Access Control (RBAC)
- User Profile Management
- Password Hashing with BCrypt
- Integration with PostgreSQL

### 2. Catalog Service

**Directory**: `services/catalog-service`

**Purpose**: Manages the product catalog, including product listing, searching, and categorization. This service allows administrators to add, update, or remove products.

**Key Features**:
- CRUD Operations for Products
- Product Search and Filtering
- Integration with PostgreSQL
- Caching with Redis (optional)

### 3. Order Service

**Directory**: `services/order-service`

**Purpose**: Manages order processing and tracking. Handles order creation, status updates, and history retrieval.

**Key Features**:
- Create and Manage Orders
- Order Tracking
- Integration with PostgreSQL
- Event-Driven Communication with Event Bus

### 4. Basket Service

**Directory**: `services/basket-service`

**Purpose**: Manages user shopping carts, allowing users to add, update, or remove items before checkout.

**Key Features**:
- Add/Remove Items to/from Basket
- Retrieve Basket Details
- Integration with Redis for Fast Access

### 5. Payment Service

**Directory**: `services/payment-service`

**Purpose**: Handles payment processing, integrating with payment gateways like Stripe or PayPal to process transactions securely.

**Key Features**:
- Payment Initiation and Processing
- Payment Status Tracking
- Integration with Payment Gateways
- Webhook Handling for Asynchronous Events

### 6. Webhook Service

**Directory**: `services/webhook-service`

**Purpose**: Handles incoming and outgoing webhook events for integrations with third-party services, such as sending notifications or triggering workflows.

**Key Features**:
- Register and Manage Webhooks
- Receive and Process Webhook Events
- Secure Webhook Endpoints

---

## Client Applications

### 1. Mobile BFF (Backend for Frontend)

**Directory**: `client-apps/mobile-bff`

**Purpose**: Serves as an intermediary between the mobile application and backend services, aggregating and simplifying API responses tailored for mobile clients.

**Key Features**:
- Aggregated API Endpoints for Mobile
- Authentication and Authorization Handling
- Optimized Data Retrieval for Mobile Performance

### 2. Web App

**Directory**: `client-apps/web-app`

**Purpose**: A Blazor WebAssembly-based web application providing a responsive and interactive user interface for browsing products, managing the basket, and processing orders.

**Key Features**:
- Product Browsing and Searching
- Shopping Cart Management
- User Authentication and Profile Management
- Order Checkout and History

---

## Shared Libraries

### 1. Event Bus

**Directory**: `shared/event-bus`

**Purpose**: Facilitates event-driven communication between microservices using RabbitMQ, enabling decoupled and scalable interactions.

**Key Features**:
- Publish and Subscribe to Events
- Event Handling Infrastructure
- Integration with RabbitMQ

### 2. Observability

**Directory**: `shared/observability`

**Purpose**: Provides centralized logging, monitoring, and tracing capabilities to ensure system reliability and ease of debugging.

**Key Features**:
- Logging with Serilog or ELK Stack
- Metrics Collection with Prometheus
- Visualization with Grafana
- Distributed Tracing with OpenTelemetry

---

## Getting Started

### Prerequisites

- [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- [PostgreSQL](https://www.postgresql.org/download/)
- [RabbitMQ](https://www.rabbitmq.com/download.html)
- [Docker](https://www.docker.com/get-started) 
- [Git](https://git-scm.com/downloads)

### Setup Instructions

1. **Clone the Repository**

    ```bash
    git clone https://github.com/felixojiambo/eshopreferenceapplication-openapi.git
    cd eshopreferenceapplication-openapi
    ```

2. **Configure Environment Variables**

    Create a `.env` file or use your preferred secrets management system to store sensitive information like database connection strings, JWT secrets, and API keys.

3. **Set Up the Database**

    Ensure PostgreSQL is installed and running. Create the necessary databases for each service (e.g., `eShopIdentity`, `eShopCatalog`, etc.).

4. **Apply Migrations**

    For each service that uses Entity Framework Core:

    ```powershell
    cd services/identity-service
    dotnet ef database update
    ```

    Repeat for other services as needed.

5. **Run RabbitMQ**

    You can run RabbitMQ using Docker:

    ```bash
    docker run -d --hostname my-rabbit --name some-rabbit -p 5672:5672 -p 15672:15672 rabbitmq:3-management
    ```

    Access RabbitMQ Management at [http://localhost:15672](http://localhost:15672) with default credentials (`guest`/`guest`).

6. **Build and Run Services**

    For each microservice:

    ```powershell
    cd services/identity-service
    dotnet run
    ```

    Repeat for other services. Ensure each service is configured with the correct connection strings and service dependencies.

7. **Run Client Applications**

    - **Web App**:

        ```powershell
        cd client-apps/web-app
        dotnet run
        ```

    - **Mobile BFF**:

        ```powershell
        cd client-apps/mobile-bff
        dotnet run
        ```

---

## Project Structure

```plaintext
eshop/
├── services/
│   ├── identity-service/
│   ├── catalog-service/
│   ├── order-service/
│   ├── basket-service/
│   ├── payment-service/
│   └── webhook-service/
├── client-apps/
│   ├── mobile-bff/
│   └── web-app/
├── shared/
│   ├── event-bus/
│   └── observability/
├── README.md
└── .gitignore
