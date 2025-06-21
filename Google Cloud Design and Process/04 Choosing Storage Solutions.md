
These notes provide a comprehensive overview of Google Cloud’s storage options, detailing their characteristics (availability, durability, scalability, consistency, cost) and use cases. It equips users with a decision-making framework to choose services like Cloud Storage, Cloud SQL, Spanner, Firestore, Bigtable, BigQuery, and Memorystore, while addressing data transfer challenges for large-scale migrations.
### Learning Objectives

- Select the appropriate Google Cloud storage service based on use case, durability, availability, scalability, and cost.
- Store binary data using **Cloud Storage**.
- Store relational data with **Cloud SQL** and **Spanner**.
- Store NoSQL data using **Firestore** and **Bigtable**.
- Cache data for fast access with **Memorystore**.
- Aggregate data for queries and reports using **BigQuery** as a data warehouse.

### Key Topics

1. **Storage Characteristics**:
    - **Availability SLAs**: Vary by service and configuration, e.g.:
        - Cloud Storage: Multi-region ≥99.95%, Regional 99.9%, Coldline 99.0%.
        - Spanner and Firestore: Multi-region and single-region 99.99%.
        - SLAs are calculated monthly based on uptime percentage.
    - **Durability**: A shared responsibility to prevent data loss.
        - Cloud Storage offers 11 nines durability; users should enable versioning.
        - Disks require scheduled snapshots; Cloud SQL supports on-demand and automated backups.
        - Spanner and Firestore provide automatic replication; users should run export jobs.
    - **Scalability**: Services scale differently:
        - Horizontal scaling: Bigtable, Spanner (add nodes).
        - Vertical scaling: Cloud SQL, Memorystore (larger machines).
        - Automatic scaling: Cloud Storage, BigQuery, Firestore (no limits).
    - **Consistency**:
        - Strong consistency (all data copies updated in a transaction): Cloud Storage, Cloud SQL, Spanner, Firestore, Bigtable (no replication).
        - Eventual consistency (asynchronous updates): Bigtable (default with replication), Memorystore replicas.
    - **Cost**:
        - Bigtable and Spanner are costlier for small datasets.
        - Firestore is cheaper per GB but charges for reads/writes.
        - Cloud Storage and BigQuery are cost-effective but limited in functionality (no database in Cloud Storage; BigQuery charges for queries).
2. **Google Cloud Storage Portfolio**:
    - **Relational**: Cloud SQL (regional, managed MySQL/PostgreSQL), Spanner (global, scalable), AlloyDB (HTAP).
    - **NoSQL**: Firestore (document database, 1 MB max per document, hierarchical data), Bigtable (infinitely scalable, high read/write for IoT, finance).
    - **Object**: Cloud Storage (schemaless, infinite scale, for images, backups).
    - **File**: Filestore (managed file storage).
    - **Block**: Persistent Disk (durable storage for VMs).
    - **Warehouse**: BigQuery (SQL-based analytics, fixed schema).
    - **In-memory**: Memorystore (managed Redis for caching).
3. **Decision Framework**:
    - A decision chart guides selection:
        - Analytics? Use BigQuery.
        - Relational data? Choose AlloyDB (HTAP), Cloud SQL (regional), or Spanner (global).
        - Non-relational? Use Memorystore (caching) or Firestore (document store).
        - File storage? Use Filestore or Cloud Storage.
    - Microservices should maintain separate data stores based on characteristics (structured/unstructured, SQL/NoSQL, consistency, data volume, read/write patterns).
4. **Data Transfer**:
    - **Challenges**: Large datasets take significant time to transfer (e.g., 1 PB at 1 Mbps takes 340 years).
    - **Cloud Storage Transfer Service**:
        - For smaller/scheduled uploads from Amazon S3, HTTP/HTTPS, or between Cloud Storage buckets.
        - Supports one-time or recurring transfers, filtering by file name or creation date.
        - For on-premises data (>1 TB), uses agents in Docker containers, requiring ≥300 Mbps bandwidth.
    - **Transfer Appliance**: For large datasets (up to 1 PB), a physical device is shipped to Google for secure data upload.
    - **BigQuery Data Transfer Service**: Automates data imports from SaaS apps (e.g., Google Ads) or sources like Amazon S3, Redshift, Teradata.
5. **Activities**:
    - **Activity 6**: Define storage characteristics (structured/unstructured, SQL/NoSQL, consistency, data volume, read/write) for case-study services.
    - **Activity 7**: Select appropriate Google Cloud storage services for case-study microservices.
    - Example for "ClickTravel" portal:
        - Inventory: Cloud Storage (JSON uploads), Firestore (processed data).
        - Orders: Cloud SQL (relational).
        - Analytics: BigQuery (data warehouse).