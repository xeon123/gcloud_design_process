These notes covers maintaining and monitoring Google Cloud applications, detailing version management (rolling updates, blue/green, canary), cost optimization (compute, disk, network, storage), and observability (monitoring, uptime checks, alerts). It emphasizes zero-downtime deployments, cost-efficient designs, and proactive monitoring to meet SLOs/SLAs. Through activities and labs, it equips users to design and manage reliable, cost-effective cloud systems, concluding the "Reliable Cloud Infrastructure: Design and Process" course.

### Learning Objectives

- Manage service updates using **rolling updates**, **blue/green deployments**, and **canary releases**.
- Forecast, monitor, and optimize costs with the **Google Cloud Pricing Calculator**, **billing reports**, and **BigQuery analysis**.
- Monitor **Service Level Objectives (SLOs)** using **Cloud Monitoring** and **Dashboards**.
- Ensure service availability with **Uptime Checks**.
- Respond to outages using **Cloud Monitoring Alerts**.

### Key Topics

1. **Managing Versions**:
    - **Microservice Considerations**: Ensure backward compatibility in microservice updates by including version in URIs, testing thoroughly, and deploying with zero downtime.
    - **Rolling Updates**:
        - Update instances one at a time behind a load balancer, suitable when multiple versions can coexist temporarily.
        - Supported in **Compute Engine** (instance groups), **Kubernetes** (default, change Docker image), and **App Engine** (automated).
    - **Blue/Green Deployments**:
        - Use two environments: **blue** (current) and **green** (new). Test green, then switch traffic; revert if issues arise.
        - Implemented via DNS (Compute Engine), pod labels (Kubernetes), or traffic splitting (App Engine).
    - **Canary Releases**:
        - Deploy a new version alongside the current one, route a small percentage of traffic to it, and monitor for errors before full rollout.
        - Supported by adding instance groups (Compute Engine), new pods with same labels (Kubernetes), or traffic splitting (App Engine).
2. **Cost Planning**:
    - **Capacity Planning**: A continuous cycle of forecasting demand, estimating capacity, deploying resources, monitoring accuracy, and adjusting.
    - **Compute Cost Optimization**:
        - Start with small VMs, enable autoscaling, and use **committed use discounts** or **Spot VMs** (60-91% savings, managed instance groups recreate preempted VMs).
        - Leverage **Google Cloud rightsizing recommendations** to identify underutilized VMs.
    - **Disk Cost Optimization**:
        - Avoid over-allocating disk space; choose disk type (Standard vs. SSD) based on I/O patterns (e.g., small/large reads/writes).
        - Example: 1TB Standard PD costs $40/month vs. $170 for SSD.
    - **Network Cost Optimization**:
        - Keep machines close to data to minimize egress costs (free within same zone, higher across regions/continents).
        - Use **Cloud CDN** or **Memorystore** for caching, or **Pub/Sub** for decoupled messaging to reduce storage needs.
    - **Cost Estimation and Monitoring**:
        - Use **Google Cloud Pricing Calculator** to estimate costs based on capacity forecasts, comparing compute/storage options.
        - Monitor with **Cloud Billing Reports** for detailed cost breakdowns by project, product, or region.
        - Export billing data to **BigQuery** for advanced analysis (e.g., identify high egress costs, optimize with CDN).
        - Visualize spend with **Looker Studio** dashboards (daily/monthly views by service/project).
        - Set **budgets and alerts** to track spending thresholds.
    - **GKE Usage Metering**:
        - Compares requested vs. consumed resources in Kubernetes clusters, exporting metrics to BigQuery for analysis to prevent over-provisioning.
    - **Storage Cost Comparison**:
        - Choose cost-effective storage (e.g., 1GB Firestore free vs. $500/month for Bigtable).
3. **Monitoring Dashboards**:
    - **Unified Tools**: Google Cloud provides **Monitoring**, **Logging**, **Trace**, **Error Reporting**, and **Profiler** to track SLOs/SLAs and diagnose issues.
    - **Dashboards**:
        - Monitor metrics like CPU, storage, reads/writes, network egress, and **Service Level Indicators (SLIs)** to ensure SLO compliance.
        - Default dashboards created for project resources; custom dashboards available.
        - Example: Charts for CPU usage and ingress traffic provide usage insights.
    - **Uptime Checks**:
        - Monitor service availability and latency (a key SRE "golden signal").
        - Example: 100% uptime with no outages, per Google’s Site Reliability Engineering (SRE) principles.
    - **Alerts**:
        - Create alerting policies for SLO violations (stricter than SLAs) to preempt SLA breaches.
        - Example: HTTP check on an instance triggers customized email alerts.
4. **Activity 13: Cost Estimating and Planning**:
    - Use the **Pricing Calculator** to estimate case study application costs.
    - Example: For ClickTravel’s database services:
        - **Cloud SQL** (Orders, with failover replica): $1,264.44/month.
        - **Firestore** (Inventory): $215.41/month.
        - **Cloud Storage** (Inventory, JSON files): $1,801.00/month (most expensive, consider storage class/lifecycle management).
        - **BigQuery** (Analytics): $214.72/month.
    - Refine estimates as capacity planning improves, especially for network egress or read/write volumes.
5. **Lab: Monitoring Applications in Google Cloud**:
    - Deploy an App Engine application and use Google Cloud tools to:
        - Examine **Cloud Logs**, view **Profiler** data, explore **Cloud Trace**.
        - Monitor resources via **Dashboards**, create **Uptime Checks**, and set **Alerts**.
    - Reinforces monitoring SLIs/SLOs to validate service performance.