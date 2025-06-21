
These notes details strategies for designing reliable Google Cloud systems, focusing on availability, durability, and scalability through fault tolerance, failure mitigation (single points, correlated, cascading, overloads), and resilient data storage (lazy deletion). It emphasizes disaster planning with cold/hot standby, RPO/RTO metrics, and regular recovery drills. Hands-on activities help apply these principles to ensure robust, recoverable systems in real-world scenarios.

### Learning Objectives

- Design services for **availability**, **durability**, and **scalability**.
- Build **fault-tolerant systems** by avoiding single points of failure, correlated failures, and cascading failures.
- Prevent **overload failures** using circuit breaker and truncated exponential backoff patterns.
- Implement **resilient data storage** with lazy deletion.
- Design for **normal, degraded, and failure states**.
- Plan, implement, and test **disaster recovery** strategies.

### Key Topics

1. **Key Performance Metrics**:
    - **Availability**: Percentage of time a system is operational.
        - Achieved via fault tolerance, backup systems, health checks, and clear box metrics (tracking real traffic success/failure).
    - **Durability**: Likelihood of data loss due to hardware/system failure.
        - Ensured by multi-zone data replication, regular backups, and restore testing.
    - **Scalability**: Ability to handle growing user load and data.
        - Supported by monitoring usage, autoscaling (using CPU, memory, or custom metrics like game server players), and capacity planning.
2. **Designing for Reliability**:
    - **Avoid Single Points of Failure**:
        - Use **N+2 redundancy** (deploy two extra units for upgrades and failures).
        - Deploy across multiple zones, ensure units are stateless clones, and verify each unit can handle increased load.
    - **Avoid Correlated Failures**:
        - Occur when related components (e.g., same rack, zone, software) fail together, forming a **failure domain**.
        - Mitigate by decoupling servers, using microservices across multiple zones/regions, and splitting responsibilities into independent components.
    - **Avoid Cascading Failures**:
        - Happen when one failure overloads others (e.g., a failing backend overloads a message queue).
        - Prevent with health checks (Compute Engine) or readiness/liveness probes (GKE), ensuring fast instance startups without backend dependencies.
    - **Query of Death Overload**:
        - Business logic errors causing resource overconsumption.
        - Mitigate with monitoring (latency, resource use, error rates) and observability to identify root causes.
    - **Positive Feedback Cycle Overload**:
        - Retries exacerbate overloads.
        - Use **truncated exponential backoff** (increasing retry delays, e.g., 1s, 2s, 4s, with limits) and **circuit breaker** patterns (proxy monitors service health, halts requests to unhealthy services, auto-implemented in GKE with Istio).
    - **Lazy Deletion**:
        - Enables data recovery after accidental deletion via phased deletion (e.g., 30-day user-recoverable period, followed by soft deletion for admin recovery, then permanent deletion).
        - Protects against user or application errors.
3. **Disaster Planning**:
    - **High Availability Strategies**:
        - Deploy to multiple zones using **regional managed instance groups** (Compute Engine) or **regional Kubernetes clusters** (GKE) with autohealing and load balancing.
        - Use health checks to verify service and backend availability, ensuring load balancers route to healthy instances.
        - For data:
            - **Cloud Storage**: Multi-region buckets (99.95% availability vs. 99.9% for single-region).
            - **Cloud SQL**: Failover replicas in another zone (doubles cost).
            - **Firestore/Spanner**: Multi-region deployments (99.99% SLA, <6 min/year downtime).
    - **Cost vs. Risk**:
        - High availability increases costs (extra resources); requires risk/cost analysis balancing deployment options (single zone, multi-zone, multi-region) against downtime costs.
    - **Disaster Recovery Strategies**:
        - **Cold Standby**: Store snapshots, machine images, and backups in multi-region storage; spin up servers in a backup region during failure (requires regular testing).
        - **Hot Standby**: Use multi-region instance groups with global load balancers, multi-region Cloud Storage, and databases like Spanner/Firestore.
        - Define **Recovery Point Objective (RPO)** (acceptable data loss) and **Recovery Time Objective (RTO)** (acceptable downtime).
        - Brainstorm failure scenarios, prioritize (e.g., high for orders, medium for analytics), and create recovery plans with backup strategies and procedures.
    - **Drills**:
        - Plan and document failure scenarios, practice recovery in test/production environments, and assess risks to balance availability costs vs. system weaknesses.
4. **Activities**:
    - **Activity 10**: Diagram application deployment for high availability, scalability, and durability.
        - Example: Online bank app with global load balancer, multi-zone/regional deployment (us-central1, us-east1), failover Cloud SQL, multi-regional Firestore, and backups in Cloud Storage.
        - ClickTravel example: Global UI in us-central1/europe-west2, regional backends in us-central1, multi-zone Orders/Inventory, single-zone Analytics, failover Cloud SQL, and multi-regional Firestore/BigQuery/Cloud Storage backups.
    - **Activity 11**: Brainstorm disaster scenarios and formulate recovery plans.
        - Example: ClickTravel scenarios include accidental Inventory deletion (RPO: 1 hour, RTO: 1 hour, high priority), Orders database crash (RPO: 0, RTO: 5 min, high), and Analytics table deletion (RPO: 0, RTO: 24 hours, medium).
        - Recovery plans: Firestore daily backups to Cloud Storage, Cloud SQL failover replica with binary logging, BigQuery data re-import.