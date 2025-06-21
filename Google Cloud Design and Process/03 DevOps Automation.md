
These notes emphasizes automation as a DevOps cornerstone, detailing Google Cloud tools for CI/CD pipelines (Cloud Source Repositories, Cloud Build, Artifact Registry, Build Triggers) and secure deployments (Binary Authorization). It also covers IaC with Terraform to create disposable infrastructure, aligning with cloud-native practices for scalability, reliability, and cost-efficiency.

### Learning Objectives:

- Automate service deployment with CI/CD pipelines.
- Use Cloud Source Repositories for version control.
- Automate builds with Cloud Build and triggers.
- Manage container images in Artifact Registry.
- Implement IaC using Terraform for disposable infrastructure.

### Key Topics Covered:

1. **DevOps Automation Overview**:
    - Automation ensures consistency, reliability, and speed in deployments, critical for DevOps and microservices.
    - Google Cloud tools support automated CI/CD pipelines and on-demand resource provisioning.
2. **Continuous Integration (CI) Pipelines**:
    - **Process**: Developers check code into a Git repository, triggering unit tests, building a deployment package (e.g., Docker image), and storing it in an artifact registry.
    - **Best Practices**: Each microservice has its own repository. Additional steps include code linting, quality analysis (e.g., SonarQube), integration tests, and image scanning.
    - **Google Cloud Tools**:
        - **Cloud Source Repositories**: Managed Git repositories with IAM access control, Pub/Sub integration, audit logging, and connectivity to GitHub/Bitbucket.
        - **Cloud Build**: Executes builds on Google Cloud, importing code from various sources and producing artifacts like Docker images. Supports custom build steps in containers.
        - **Build Triggers**: Automatically start builds on code changes, configurable for specific criteria.
        - **Artifact Registry**: Stores Docker/OCI images and other artifacts, integrates with CI/CD tools, supports vulnerability scanning, and uses IAM for access control.
3. **Binary Authorization**:
    - Ensures only trusted containers are deployed to Google Kubernetes Engine (GKE).
    - Requires enabling binary authorization on GKE clusters, defining policies for signed images, and using an attestor to verify image sources (e.g., Cloud Source Repositories).
    - Artifact Registry’s vulnerability scanner and Pub/Sub notifications support this process via the Kritis Signer.
4. **Infrastructure as Code (IaC)**:
    - **Cloud Mindset**: Unlike on-premises (buying large, long-running machines), cloud infrastructure is rented, disposable, and scaled out with smaller machines treated as operating expenses.
    - **IaC Principles**: Automate provisioning to eliminate manual errors, ensure repeatability, and support ephemeral environments. Avoid fixing or patching machines; instead, recreate them.
    - **Benefits**: Enables on-demand provisioning, identical environments (dev/test/prod), disaster recovery, and integration with CI/CD pipelines.
    - **Tools**: Google Cloud supports Terraform, Chef, Puppet, Ansible, and Packer.
5. **Terraform**:
    - An IaC tool for repeatable, declarative infrastructure provisioning across multiple clouds.
    - **Features**: Uses a configuration file to define resources (e.g., VMs, networks), supports parallel deployments, and modular templates.
    - **Syntax**: Includes blocks (for resources), arguments (name-value pairs), and expressions (values).
    - **Google Cloud Integration**: Pre-installed in Cloud Shell, supports Google Cloud resources via provider blocks (e.g., Compute Engine instances).
    - Example: A configuration file defines a Google Cloud network or VM with specified attributes and outputs (e.g., instance IP).
6. **Lab: Building a DevOps Pipeline**:
    - **Objective**: Create a CI pipeline using Cloud Source Repositories, Cloud Build, and Artifact Registry.
    - **Tasks**:
        - Set up a Git repository and add a Python web application.
        - Test the application in Cloud Shell and define a Docker build.
        - Use Cloud Build to create and store a Docker image in Artifact Registry.
        - Configure build triggers to automate builds on code changes and test by pushing updates.
    - **Outcome**: Demonstrates automation of Docker image creation and storage, with testing on a Compute Engine VM.