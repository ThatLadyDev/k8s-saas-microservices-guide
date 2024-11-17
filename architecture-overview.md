# Explanation of the microservice architecture and flow

This document provides an overview of the architecture used for the multi-tenant SaaS platform, which is built using microservices. Each service in the platform works independently but is designed to communicate with other services via RESTful APIs, ensuring scalability and maintainability. Kubernetes is used to orchestrate the microservices in a production environment.

## Multi-Tenant SaaS Architecture

The SaaS platform is designed to serve multiple tenants, with each tenant being logically isolated while sharing the same infrastructure. This is achieved by implementing tenant-specific configurations and ensuring that each tenant's data and resources are kept separate.

### Services Overview

The platform consists of the following microservices, all of which are built using **Laravel** for rapid development:
1. **Autho-SaaS**  
   - **Role**: Handles user authentication, user roles, and tenant management.
   - **Responsibility**: Manages the registration, login, and access control for tenants and their users.

2. **Billify-SaaS**  
   - **Role**: Handles billing and subscription management for each tenant.
   - **Responsibility**: Manages the creation of invoices, payment processing, and subscription plans.

3. **Notifi-SaaS**  
   - **Role**: Manages notifications and alerts for tenants.
   - **Responsibility**: Sends event-driven notifications (email, SMS, etc.) to users based on tenant-specific configurations.

4. **API Middleware (API Gateway)**  
   - **Role**: Serves as the central entry point for all external requests to the platform.
   - **Responsibility**: The API middleware application receives API requests and routes them to the appropriate microservice (e.g., **Autho-SaaS**, **Billify-SaaS**). It is responsible for handling tenant-specific requests by routing them to the right service based on the `tenant_uuid` in the API request.

5. **Database Service (MySQL)**  
   - **Role**: Manages the database connections and queries for all services.
   - **Responsibility**: Handles requests and queries related to tenant-specific data, ensuring the isolation and integrity of data for each tenant. The **MySQL service** is designed to scale horizontally to support the growth of the SaaS platform and ensure optimal performance across all services.

6. **Mailing Service (Mailpit)**  
   - **Role**: Traps and stores emails sent from the application in the local development environment.
   - **Responsibility**: **Mailpit** is used to capture email communications in the development environment, allowing developers to inspect email content and troubleshoot email delivery without actually sending real emails. In production, a dedicated mailing service (e.g., **SMTP** or **SendGrid**) would be used, but **Mailpit** ensures that emails are captured for local testing.

### Tenant Isolation Strategy

The platform uses **logical isolation** for each tenant, meaning that each tenant shares the same physical infrastructure but has its own isolated environment within the microservices. This is done using strategies like:

- **Tenant UUID**: Each request includes a `tenant_uuid`, which ensures that the correct tenant data is accessed across the microservices.
- **Service Level Isolation**: Services use tenant-specific configurations and databases to ensure that data and resources are isolated for each tenant.

### API Middleware Layer (Service)

The **API Middleware** (sometimes referred to as the **API Gateway**) is an important part of the architecture, serving as the **central service** that handles all incoming API requests. The API middleware is defined in the **Docker Compose** file and is also included in the **Kubernetes deployment** configuration, meaning it is deployed alongside the other services. 

The responsibilities of the API middleware are:

- **Request Routing**: The API middleware receives incoming API requests from external clients. It inspects the request, identifies the appropriate backend service (e.g., **Autho-SaaS**, **Billify-SaaS**), and forwards the request accordingly.
- **Security and Rate Limiting**: The API middleware adds an extra layer of security by preventing direct access to backend services. It helps mitigate security risks by controlling access to the backend services and provides logging, monitoring, and rate-limiting features.
- **Tenant Identification**: By examining the `tenant_uuid` passed in the request headers or parameters, the API middleware ensures the request is routed to the correct tenant's data within the appropriate service.
- **Centralized Authentication**: The middleware interacts with the **Autho-SaaS** service for authentication, managing tokens, and authorizing requests before forwarding them to backend services.
  
This service is defined within both the **Docker Compose** and **Kubernetes** configurations, ensuring it runs in both local and production environments, where it acts as the gatekeeper for all external traffic.

### Backend Services - Built with Laravel

All the backend microservices (Autho-SaaS, Billify-SaaS, Tenantrix-SaaS, Notifi-SaaS) are built using **Laravel**, a PHP framework that offers:

- **Rapid Development**: Laravel is known for its ease of use and its ability to rapidly build robust applications, which allows the team to quickly iterate and deliver new features.
- **Built-in Features**: Laravel provides built-in features like authentication, routing, database migrations, and a task scheduler, making it a great choice for building microservices that need to scale.
- **Service-Oriented Architecture**: Laravel’s architecture supports building scalable services with clean separation of concerns, making it ideal for a microservices-based design.

### Kubernetes-Based Orchestration

Kubernetes is used to manage the deployment, scaling, and management of the microservices. The key aspects of Kubernetes in this architecture include:

- **Namespaces**: Each microservice, including the **API Middleware**, is deployed within its own namespace in Kubernetes, ensuring that their configurations and secrets are logically isolated.
- **Resource Limits**: Kubernetes resource quotas are used to allocate specific resources (e.g., CPU, memory) to each service, ensuring efficient resource usage.
- **Load Balancing**: Kubernetes' built-in load balancer ensures that traffic is evenly distributed to all instances of each microservice, enabling high availability.
- **Autoscaling**: Kubernetes can automatically scale services based on demand, ensuring that the platform can handle fluctuations in tenant usage.

### Service Interactions

The services in this architecture communicate with each other primarily via REST APIs. Below is an overview of how the services interact:

1. **Autho-SaaS**  
   - Exposes authentication endpoints that are used by other services to validate tenant users.
   - Provides an API to create and manage tenants, as well as manage roles and permissions.

2. **Billify-SaaS**  
   - Consumes the Autho-SaaS API to identify and manage tenant users.
   - Provides APIs for generating invoices, processing payments, and managing subscriptions.

3. **Notifi-SaaS**  
   - Consumes data from Tenantrix-SaaS to determine which notifications should be sent to a specific tenant.
   - Uses the Autho-SaaS service to verify user identities and determine which users should receive notifications.

4. **API Middleware (API Gateway)**  
   - Central service that routes requests to appropriate microservices, authenticates requests, and handles tenant-specific data flows.

5. **Database Service (MySQL)**  
   - Provides all database connections and handles queries for all backend services, ensuring tenant data is securely stored and retrieved.
   
6. **Mailing Service (Mailpit)**  
   - Captures email messages sent from the application in the local development environment for inspection, debugging, and troubleshooting email delivery.

### Security Considerations

Security is a key focus, especially with a multi-tenant architecture. The following measures are implemented:

- **Authentication and Authorization**:  
  OAuth 2.0 and JWT tokens ensure secure, authenticated communication between services.

- **Data Encryption**:  
  Data is encrypted in transit (via HTTPS) and at rest (via database encryption) to protect sensitive information.

- **Tenant Data Isolation**:  
  Each tenant’s data is isolated using tenant-specific configurations, preventing unauthorized access between tenants.

- **API Middleware**:  
  The **API Middleware** acts as the only external-facing service, routing requests to the backend services. This ensures that backend services are not directly exposed to external traffic.

- **Backend Service Isolation**:  
  Except for the API Middleware, backend services are not accessible externally. They are only reachable within the internal network, enhancing security by limiting access to authorized services.

### Diagrams

The following diagrams illustrate the overall architecture, service interactions, and flow of data in the platform.

1. **Microservice Architecture**  
   ![Microservice Architecture](diagrams/microservice-architecture.png)

2. **Tenant Data Flow**  
   ![Tenant Data Flow](diagrams/tenant-data-flow.png)

3. **API Middleware Flow**  
   ![API Middleware Flow](diagrams/api-middleware-flow.png)

