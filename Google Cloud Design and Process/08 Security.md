These notes emphasizes a security-first approach, detailing Google Cloud’s shared responsibility model, layered security, and best practices (least privilege, separation of duties, audits). It covers securing users (IAM, IAP, Identity Platform), machines (service accounts), networks (private IPs, firewalls, Cloud Armor), and data (encryption, DLP). The activity helps apply these principles to design secure systems for real-world applications like ClickTravel, ensuring robust, compliant cloud environments.

### Learning Objectives

- Design secure systems using **separation of concerns**, **principle of least privilege**, and **regular audits**.
- Use **Security Command Center** to identify vulnerabilities.
- Simplify governance with **organization policies** and **folders**.
- Authenticate/authorize users via **IAM roles**, **Identity-Aware Proxy (IAP)**, and **Identity Platform**.
- Manage machine/process access with **service accounts**.
- Secure networks using **private IPs**, **firewalls**, and **Private Google Access**.
- Mitigate **DDoS attacks** with **Cloud DNS** and **Google Cloud Armor**.
- Implement **encryption** for data protection.

### Key Topics

1. **Security Concepts**:
    - **Shared Responsibility**: Google secures lower layers (hardware, boot, OS), while customers handle application, deployment, and usage security. Transparency ensures clear delineation of responsibilities.
    - **Layered Security**: Google provides tools (e.g., firewall rules, IAM) for secure environments, with options to integrate third-party tools and monitor/audit networks.
    - **Best Practices**:
        - **Principle of Least Privilege**: Grant minimal permissions to users, machines, and processes using IAM roles and service accounts.
        - **Separation of Duties**: Prevent single-person control over sensitive tasks (e.g., code writing vs. deployment) using multiple projects and folders.
        - **Regular Audits**: Monitor **admin**, **data access**, **VPC flow**, **firewall**, and **system logs** to detect attacks.
    - **Compliance**: Google Cloud meets standards like ISO/IEC 27001, HIPAA, SOC 1, but applications built on it require separate certification.
    - **Security Command Center**: Provides a dashboard for security health analysis, threat detection, anomaly detection, and actionable recommendations.
2. **Securing People**:
    - **IAM Policies**:
        - Add users as members with roles (predefined preferred over custom) via Cloud Console.
        - Assign roles to Google Groups for easier management, ensuring granular control and minimal scope (avoid overuse of "owner" or "editor" roles).
        - Policies inherit from organization to folders, projects, and resources.
    - **Identity-Aware Proxy (IAP)**: Enables secure access to App Engine, Compute Engine, or GKE applications without VPNs, requiring user login and admin-controlled access.
    - **Identity Platform**: Provides customer identity management with federated login (SAML, OpenID, Google, Twitter, etc.) for end-user sign-up/sign-in.
3. **Securing Machine Access**:
    - **Service Accounts**:
        - Used for application/VM/GKE node pool identities to make authorized API calls.
        - Assign IAM roles to control resource access; grant **ServiceAccountUser** role to trusted users.
        - Generate JSON keys for authentication (e.g., for gcloud CLI or CI/CD pipelines), stored securely as they are powerful credentials.
4. **Network Security**:
    - **Private IPs**: Remove external IPs to prevent unauthorized access; use **bastion hosts**, **IAP for SSH**, or **Cloud NAT** for egress to the internet.
    - **Private Google Access**: Enables VMs with internal IPs to access Google Cloud services (e.g., Cloud Storage) without public IPs.
    - **Firewall Rules**: Default ingress denial; configure rules for specific IPs, protocols, and ports for VM-to-VM, VM-to-external, or load balancer scenarios.
    - **Cloud Endpoints**: Manages APIs with access control, JSON Web Tokens, Google API keys, and Identity Platform integration.
    - **TLS**: Enforce HTTPS for all service endpoints, configure secure frontends for load balancers.
    - **DDoS Protection**:
        - Global load balancers and Cloud CDN drop attacks or cache hits to protect backends.
        - **Google Cloud Armor**: Creates network security policies (allow/deny lists by IP) and Layer 7 WAF rules to block attacks like SQL injection or XSS using request headers, geolocation, or custom expressions.
5. **Encryption**:
    - **Default Encryption**: Data at rest encrypted with AES-256 Data Encryption Keys (DEKs), wrapped by Key Encryption Keys (KEKs) in Cloud KMS, with automatic rotation and transparent decryption.
    - **Customer-Managed Encryption Keys (CMEK)**: Create and manage keys in Cloud KMS for compliance, specifying rotation frequency (default 90 days), used for storage resources like buckets/disks.
    - **Customer-Supplied Encryption Keys (CSEK)**: On-premises keys provided via API calls, cached in RAM for decryption, supported by Cloud Storage and Compute Engine.
    - **Data Loss Prevention (DLP) API**: Scans Cloud Storage, BigQuery, Firestore, or images for sensitive data (e.g., credit cards, SSNs) and redacts via masking, tokenization, or hashing.
6. **Activity 12: Modeling Secure Google Cloud Services**:
    - Diagram security requirements for a case study.
    - Example: Custom VPC with subnets in us-central1 (primary) and us-east1 (backup), firewall rules allowing HTTPS ingress and SSH from known sources, and Google Cloud Armor on a global load balancer to block denied IPs.
    - ClickTravel example: Similar setup with additional europe-west2 subnet, Cloud VPN for on-premises reporting, Private Google Access for backend services (Inventory, Orders, Analytics), and no external IPs for backends to reduce costs and enhance security.