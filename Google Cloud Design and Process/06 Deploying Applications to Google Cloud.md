These notes outlines Google Cloud’s deployment platforms—Compute Engine, GKE, Cloud Run, App Engine, and Cloud Run Functions—detailing their use cases, management levels, and configurations. It provides a decision framework for selecting platforms based on application needs and emphasizes best practices like 12-factor methodology for portable, scalable deployments. The lab reinforces these concepts through practical application deployment.

### Key Topics

1. **Choosing a Deployment Platform**:
    - Decision framework:
        - **Specific machine/OS requirements**: Use **Compute Engine** for full control.
        - **Containerized apps**: Choose **Google Kubernetes Engine (GKE)** for custom Kubernetes clusters or **Cloud Run** for managed container deployment.
        - **Non-containerized apps**: Use **Cloud Run functions** for event-driven services or **App Engine** for other microservices.
    - The choice depends on control, scalability, and management needs.
2. **Compute Engine (IaaS)**:
    - Ideal for applications requiring complete control over OS, non-containerized apps, microservices, or self-hosted databases.
    - **Managed Instance Groups**:
        - Create VMs using instance templates (define image, machine type, startup scripts, etc.).
        - Support autoscaling for variable workloads, autohealing via health checks, and multi-zone deployment for high availability.
    - Use as backends for load balancers (global for multi-region, enable Cloud CDN for static content, SSL for external services, no public IP for internal services).
3. **Google Kubernetes Engine (GKE)**:
    - Managed environment for containerized applications using Kubernetes.
    - Clusters consist of Compute Engine VMs (nodes) running pods (containing Docker containers).
    - Optimizes resource use by deploying multiple services in one cluster.
    - Offers **Autopilot** (fully managed) and **Standard** modes for flexibility.
    - Balances customization, portability, and cost optimization.
4. **Cloud Run**:
    - Fully managed platform for deploying stateless, containerized applications.
    - Deploys container images from **Artifact Registry** or directly from source (auto-containerizes code).
    - Revisions are immutable; supports Google Cloud Console or gcloud command-line deployment.
    - Simplifies Kubernetes management, handling load balancers, autoscalers, and health checks.
5. **App Engine**:
    - Fully managed, serverless platform for microservices.
    - Structure: One App Engine app per project, with multiple services, versions, and instances.
    - Supports traffic splitting for canary/A-B testing.
    - Example architecture: Retail app with App Engine as frontend, Cloud Storage for static content, Cloud SQL for relational data, Firestore for NoSQL, Memcache for caching, and Cloud Tasks for asynchronous processing.
6. **Cloud Run Functions**:
    - Designed for event-driven, loosely coupled microservices.
    - Triggered by Cloud Storage bucket changes, Pub/Sub messages, or HTTP requests.
    - Fully managed, scalable, and cost-effective (billed per 100ms of execution, free when idle).
    - Example: Image translation service using Vision API and Translation API, triggered by Cloud Storage uploads and Pub/Sub messages.
7. **Lab Activities**:
    - Deploy applications to **App Engine**, **GKE**, and **Cloud Run** using Dockerized code from Cloud Build (stored in Container Registry).
    - Emphasizes **12-factor app principles** for portability across platforms and providers.
    - Highlights automation with CI/CD and infrastructure-as-code for flexible deployments.
