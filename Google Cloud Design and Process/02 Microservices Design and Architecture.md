These notes provides a comprehensive guide to designing microservice architectures, emphasizing modularity, scalability, and loose coupling. It contrasts microservices with monoliths, outlines challenges and best practices (via the 12-factor app), and details RESTful API design for consistent, independent services. Google Cloud tools and standards like OpenAPI and gRPC are highlighted to support implementation.

## Learning Objectives:

- Decompose monolithic applications into microservices with clear boundaries.
- Architect stateful and stateless services for scalability and reliability.
- Apply 12-factor best practices for cloud-native development.
- Design loosely coupled, consistent RESTful APIs.

## Key Topics Covered

- **Microservices Overview**:
    - **Definition**: Microservices break a large application into smaller, independent services, unlike monolithic applications with a single codebase and database.
    - **Benefits**: Enable independent team workflows, faster deployment cycles, and independent scaling. Support diverse languages, frameworks, and runtimes.
    - **Challenges**: Increased complexity in inter-service communication, latency, security, versioning, and maintaining backward compatibility.
    - **Google Cloud Services**: App Engine, Cloud Run, GKE, and Cloud Run Functions support microservice deployment.
- **Decomposing Applications**:
    - **Service Boundaries**: Use domain-driven design to identify functional groupings (e.g., reviews, orders, products for an online store). Minimize dependencies by decomposing by feature.
    - **Shared Services**: Common services like authentication are isolated and deployed separately.
    - **Activity 4**: Diagram microservices for a case study, considering boundaries and state management (e.g., online banking or travel portal).
- **State Management**:
    - **Stateless Services**: Easier to scale and manage as they rely on external data sources.
    - **Stateful Services**: Harder to scale and upgrade, requiring persistent storage (e.g., Firestore, Cloud SQL) and caching (e.g., Memorystore for Redis).
    - **Best Practices**: Avoid in-memory shared state to prevent sticky sessions and enable autoscaling. Use backend storage services for state management.
- **Microservice Best Practices (12-Factor App)**:
    - A set of principles for building scalable, portable cloud-native applications:
        1. **Codebase**: Use version control (e.g., Git, Cloud Source Repositories).
        2. **Dependencies**: Declare and isolate dependencies (e.g., Maven, Pip, Artifact Registry).
        3. **Config**: Store configuration in environment variables.
        4. **Backing Services**: Access services (e.g., databases) via URLs.
        5. **Build, Release, Run**: Separate stages for deployment with identifiable artifacts.
        6. **Processes**: Run apps as stateless processes.
        7. **Port Binding**: Expose services via ports, bundling web servers.
        8. **Concurrency**: Scale out via processes.
        9. **Disposability**: Ensure fast startup and graceful shutdown.
        10. **Dev/Prod Parity**: Keep environments consistent using containers and tools like Terraform.
        11. **Logs**: Treat logs as event streams, writing to standard output.
        12. **Admin Processes**: Run one-off tasks as automated processes (e.g., Cloud Scheduler).
- **REST Architecture**:
    - **Loose Coupling**: Services communicate via HTTPS with text-based payloads (JSON/XML) using HTTP verbs (GET, POST, PUT, DELETE). Strong, versioned contracts prevent breaking clients.
    - **Resources and Representations**: Resources are abstract (e.g., a pet), with representations as data (e.g., JSON of a specific pet). URIs use singular/plural nouns (e.g., /pet/1, /pets).
    - **HTTP Requests/Responses**: Requests include verbs, URIs, headers, and bodies. Responses include status codes (200 for success, 400 for client errors, 500 for server errors).
    - **Best Practices**: Maintain backward compatibility, use consistent naming, and consider caching. Standards like OpenAPI or gRPC (for binary communication) support loose coupling.
- **API Design**:
    - **Consistency**: Follow Google Cloud’s API design guide for uniform interfaces (e.g., service.collection.verb format, like Compute Engine’s /compute/v1/projects/{project}/zones/{zone}/instances).
    - **OpenAPI**: Industry standard for describing REST APIs, enabling tools and humans to understand services without source code.
    - **gRPC**: Lightweight, high-performance binary protocol for internal communication, supported by Google Cloud services like Application Load Balancer and Cloud Endpoints.
    - **API Management Tools**: Cloud Endpoints, Apigee, and API Gateway provide authentication, monitoring, and security for APIs.
    - **Activity 5**: Design REST APIs for case study microservices, focusing on URL structure, request/response formats, and versioning (e.g., APIs for an online store or travel portal).