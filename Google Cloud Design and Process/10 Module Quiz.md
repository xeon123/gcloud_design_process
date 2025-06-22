## Defining Services

### 1️⃣ **Which most accurately describes a user story?**

✅ **Correct answer:**  
➡️ **It is a short description of a feature written from the user's point of view.**

**Explanation:**  
A user story is an Agile artifact that describes a desired feature or functionality _from the perspective of an end user_. It usually follows the format: _“As a [type of user], I want [some goal] so that [reason].”_  
It is not a detailed narrative of steps (that would be closer to a use case), nor just a general description of a person.

---

### 2️⃣ **Using SMART criteria, which below would be the least effective KPI?**

✅ **Correct answer:**  
➡️ **User experience design**

**Explanation:**  
SMART means: **Specific, Measurable, Achievable, Relevant, Time-bound**.

- _User sign ups per month_, _Page views per hour_, and _Clicks per session_ are all quantifiable and time-bound.
    
- _User experience design_ is vague and not inherently measurable as a KPI on its own. It needs to be operationalized (e.g., through usability scores, task success rate, etc.) to be SMART.
    

---

### 3️⃣ **Which best describes an SLO?**

✅ **Correct answer:**  
➡️ **It is a target measure you want your service to achieve.**

**Explanation:**  
An **SLO (Service Level Objective)** is a clearly defined target or goal for the level of service performance (e.g., “99.9% availability over 30 days”).  
It is _not_ a contract with users — that would be an SLA (Service Level Agreement). It’s also not an individual KPI or a feature description.
## Microservices Design and Architecture

### ✅ 1️⃣ **You’re building a RESTful microservice. Which would be a valid data format for returning data to the client?**

➡️ **Correct answer:**  
✔ **All options are correct.**

**Explanation:**  
A RESTful service can return data in **JSON** (most common), **XML** (common in some enterprise systems), or even **HTML** (e.g., if rendering a webpage). The format depends on the `Accept` header from the client and what the service supports. So technically, all listed formats are valid.

---

### ✅ 2️⃣ **You’ve re-architected a monolithic web application so state is not stored in memory on the web servers, but in a database instead. This has caused slow performance when retrieving user sessions though. What might be the best way to fix this?**

➡️ **Correct answer:**  
✔ **Use a caching service like Memorystore for Redis.**

**Explanation:**  
Databases are slower than in-memory storage for session data. Using a dedicated cache like **Redis** or **Memcached** is a best practice for session storage: you get fast, in-memory reads/writes, but still keep your servers stateless.

---

### ✅ 3️⃣ **You’re writing a service, and you need to handle a client sending you invalid data in the request. What should you return from the service?**

➡️ **Correct answer:**  
✔ **A 400 error code**

**Explanation:**  
A **400 Bad Request** means “the request was malformed or contained invalid data”. It’s the appropriate response for client-side input errors.  
A 500 would mean _server-side_ error.

---

### ✅ 4️⃣ **Which below would violate 12-factor app best practices?**

➡️ **Correct answer:**  
✔ **Store configuration information in your source repository for easy versioning.**

**Explanation:**  
According to the 12-factor app guidelines, **config should be stored in environment variables**, _not in source code_.

- Dependencies must be declared and isolated ✅
    
- Environments should be as similar as possible ✅
    
- Logs treated as event streams ✅  
    Storing config in code violates the principle of strict separation of config and code.
## DevOps Automation

### ✅ 1️⃣ **Which Google Cloud tools can be used to build a continuous integration pipeline?**

➡️ **Correct answer:**  
✔ **All of these**

**Explanation:**  
All the listed tools can play a role in a CI pipeline:

- **Cloud Source Repositories** → to store and version your source code.
    
- **Cloud Build** → to run build/test steps automatically.
    
- **Artifact Registry** → to store build artifacts (e.g., container images, packages).  
    Together, they cover **code, build, and artifact storage** — which is exactly what a CI pipeline needs.
    

---

### ✅ 2️⃣ **What Google Cloud feature would be easiest to use to automate a build in response to code being checked into your source code repository?**

➡️ **Correct answer:**  
✔ **Build triggers**

**Explanation:**  
**Build triggers** are designed specifically for this: they automatically start a **Cloud Build** job whenever changes are pushed to a connected repo.  
The other options don’t directly provide build automation:

- **Cloud Run functions** run code containers.
    
- **App Engine** runs apps.
    
- **Cloud Scheduler** runs jobs on a time schedule, not on repo events.
## Storage Solutions

### ✅ 1️⃣ **Currently, you are using Firestore to store information about products, reviews, and user sessions. You'd like to speed up data access in a simple, cost-effective way. What would you recommend?**

➡️ **Correct answer:**  
✔ **Cache the data using Memorystore.**

**Explanation:**  
Firestore is good for flexible, serverless NoSQL storage — but adding a caching layer like **Memorystore (Redis)** is the simplest, most cost-effective way to reduce read latency and speed up frequent lookups, without re-architecting your database.

---

### ✅ 2️⃣ **You are a global financial services company with users all over the world. You need a database service that can provide low latency worldwide with strong consistency. Which service might you choose?**

➡️ **Correct answer:**  
✔ **Spanner**

**Explanation:**  
**Spanner** is Google Cloud’s globally distributed SQL database — designed to deliver low-latency reads/writes across the globe **with strong consistency** (which is very rare at global scale). It’s purpose-built for use cases like multi-region financial services.

---

### ✅ 3️⃣ **You want to analyze sales trends. To help achieve this, you want to combine data from your on-premises Oracle database with Google Analytics data and your web server logs. Where might you store the data so it is both easy to query and cost-effective?**

➡️ **Correct answer:**  
✔ **BigQuery**

**Explanation:**  
**BigQuery** is Google’s serverless data warehouse, designed exactly for combining and analyzing large amounts of structured and semi-structured data from multiple sources. It’s cost-effective because you pay for what you query and don’t manage infrastructure.

---

### ✅ 4️⃣ **You need to store user preferences, product information, and reviews for a website you are building. There won't be a huge amount of data. What would be a simple, cost-effective, managed solution?**

➡️ **Correct answer:**  
✔ **Firestore**

**Explanation:**  
**Firestore** is a fully managed NoSQL document database, perfect for storing JSON-like objects like user preferences, product details, and reviews. It scales automatically and has low cost for small workloads — ideal for websites and mobile apps with modest data needs.

## Google Cloud and Hybrid Network Architecture

### ✅ 1️⃣ **You want a secure, private connection between your network and a Google Cloud network. There is not a lot of volume, but the connection needs to be extremely reliable. Which configuration below would you choose?**

➡️ **Correct answer:**  
✔ **VPN with high availability and Cloud Router**

**Explanation:**

- **Cloud VPN** is ideal for secure, private connections when traffic volume is low to moderate.
    
- Adding **high availability (HA VPN)** and **Cloud Router** ensures dynamic routing and redundancy for reliability.
    
- **Cloud Interconnect** is better for high-volume, dedicated bandwidth (but overkill here).
    
- **VPC peering** only works between Google Cloud VPCs — not for connecting your on-prem network to Google Cloud.
    

---

### ✅ 2️⃣ **You are a large bank deploying an online banking service to Google Cloud. The service needs high volume access to mainframe data on-premises. Which connectivity option would likely be most suitable?**

➡️ **Correct answer:**  
✔ **Cloud Interconnect**

**Explanation:**  
**Cloud Interconnect** provides a dedicated, high-bandwidth, low-latency connection between your on-premises network and Google Cloud.  
This is ideal for large volumes of traffic to sensitive systems like mainframes — more stable and performant than VPN.

---

### ✅ 3️⃣ **You are deploying a large-scale web application with users all over the world and a lot of static content. Which load balancer configuration would likely be the most suitable?**

➡️ **Correct answer:**  
✔ **Application Load Balancer with SSL configured and the CDN enabled**

**Explanation:**

- The **Application Load Balancer** (HTTP(S) Load Balancer) is a global, Layer 7 load balancer designed for web applications.
    
- Enabling the **CDN** ensures caching of static content close to users worldwide for faster delivery.
    
- SSL ensures secure connections.
    

Network Load Balancer is Layer 4 — not optimal for web apps needing content delivery optimization.

---

### ✅ 4️⃣ **You have a contract with a service provider to manage your Google VPC networks. You want to connect a network they own to your VPC. Both networks are in Google Cloud. Which Connection option should you choose?**

➡️ **Correct answer:**  
✔ **VPC peering**

**Explanation:**  
**VPC peering** directly connects two VPC networks in Google Cloud, allowing private IP traffic between them without using external IPs, VPNs, or Interconnect.  
It’s simple, low-latency, and cost-effective for internal GCP-to-GCP network connections.

## Deploying Applications to Google Cloud

### ✅ 1️⃣ **You have containerized multiple applications using Docker and have deployed them using Compute Engine VMs. You want to save on costs and simplify container management. What might you do?**

➡️ **Correct answer:**  
✔ **Migrate the containers to GKE**

**Explanation:**

- **GKE (Google Kubernetes Engine)** is designed for orchestrating and managing multiple containers more efficiently than manually running them on Compute Engine VMs.
    
- It provides automated scaling, scheduling, and management, which reduces costs and operational overhead.
    
- Rewriting to App Engine or Cloud Run would require changes to how your containers run; GKE can use your existing Docker images directly.
    

---

### ✅ 2️⃣ **You need to deploy an existing application that was written in .NET version 4. The application requires Windows servers, and you don't want to change it. Which should you use?**

➡️ **Correct answer:**  
✔ **Compute Engine**

**Explanation:**

- **Compute Engine** lets you provision Windows Server VMs where you can run legacy .NET Framework apps without rewriting them.
    
- App Engine, Cloud Run, and GKE are optimized for Linux containers and modern runtimes, not for old Windows workloads.
    

---

### ✅ 3️⃣ **You've been asked to write a program that uses Vision API to check for inappropriate content in photos that are uploaded to a Cloud Storage bucket. Any photos that are inappropriate should be deleted. What might be the simplest, cheapest way to deploy this program?**

➡️ **Correct answer:**  
✔ **Cloud Run functions**

**Explanation:**

- **Cloud Run (or Cloud Functions)** is serverless, automatically scales, and is cost-effective for event-driven tasks like reacting to file uploads.
    
- It’s easy to set up a trigger on Cloud Storage, run the Vision API check, and delete the file if needed.
    
- GKE, App Engine, or Compute Engine are overkill for a simple event-driven program.

## Designing Reliable Systems

### ✅ 1️⃣ **You need a relational database for a system that requires extremely high availability (99.999%). The system must run uninterrupted even in the event of a regional outage. Which database would you choose?**

➡️ **Correct answer:**  
✔ **Spanner**

**Explanation:**

- **Spanner** is Google Cloud’s globally distributed SQL database with strong consistency and **multi-region replication**, designed for extremely high availability (up to **99.999% SLA**).
    
- **Cloud SQL** is zonal/regionally redundant but doesn’t reach that level of global HA.
    
- **Firestore** is NoSQL, not relational.
    
- **BigQuery** is an analytical data warehouse, not for transactional relational workloads.
    

---

### ✅ 2️⃣ **You're creating a service and you want to protect it from being overloaded by too many client retries in the event of a partial outage. Which design pattern would you implement?**

➡️ **Correct answer:**  
✔️ **Circuit breaker**

**Detailed explanation:**

- **Truncated exponential backoff** is a _client-side_ pattern for retrying **more gracefully**, spreading out retries.
    
- **Circuit breaker** is a _service-side_ resilience pattern: it **detects failures and opens the circuit** to block calls temporarily — preventing the backend from being overloaded when it’s degraded.
    
- In practice, both are complementary — but **the circuit breaker directly protects the service** by rejecting requests fast once a threshold is crossed.

## Security

### ✅ 1️⃣ **What do you have to do to enable encryption when using Cloud Storage?**

➡️ **Correct answer:**  
✔ **Nothing as encryption is enabled by default.**

**Explanation:**  
All data stored in Google Cloud Storage is **encrypted at rest by default** using Google-managed encryption keys. You can optionally use **customer-managed keys** (via Cloud KMS) or **customer-supplied keys**, but you do **not** need to do anything to have encryption — it’s automatic.

---

### ✅ 2️⃣ **Which Google Cloud features could help reduce the risk of DDoS attacks?**

➡️ **Correct answer:**  
✔ **All of these**

**Explanation:**  
All listed services contribute to DDoS protection:

- **Google Cloud Armor**: provides configurable WAF rules and DDoS mitigation.
    
- **Cloud CDN**: caches content at the edge, absorbing large spikes in requests.
    
- **Global external Application Load Balancer**: distributes traffic across global backends, helping handle large loads gracefully.
    

Combined, they form a robust DDoS defense.

---

### ✅ 3️⃣ **You don't want programmers to have access to production resources. What's the easiest way to do this in Google Cloud?**

➡️ **Correct answer:**  
✔ **Create development and production projects, and don't give developers access to production.**

**Explanation:**  
The simplest and most secure approach is to use **separate GCP projects** for dev and prod, and restrict IAM permissions accordingly. This cleanly isolates environments and access control.

---

### ✅ 4️⃣ **What Google Cloud service can you use to enforce the principle of least privilege when using Google Cloud?**

➡️ **Correct answer:**  
✔ **IAM members and roles**

**Explanation:**  
**IAM (Identity and Access Management)** lets you define who can do what on which resources. By granting **only the minimum roles needed**, you enforce the **least privilege principle**.  
SSL, encryption keys, and firewall rules help with security, but IAM directly controls access rights.

## Maintenance and Monitoring

### ✅ 1️⃣ **You made a minor update to a service and would like to test it in production by sending a small portion of requests to the new version. Which would you choose?**

➡️ **Correct answer:**  
✔ **Canary deployment**

**Explanation:**  
A **canary deployment** rolls out a new version to a small percentage of production traffic. This lets you test real-world behavior with minimal risk before a full rollout.

- Rolling update: gradually replaces instances but doesn’t explicitly test on a subset.
    
- Blue/green: swaps the entire environment.
    
- A/B test: tests two different features/variations for comparison, not usually for gradual rollout.
    

---

### ✅ 2️⃣ **Your service has an availability SLO of 99%. What could you use to monitor whether you are meeting it?**

➡️ **Correct answer:**  
✔ **Uptime check**

**Explanation:**  
An **uptime check** continuously verifies if your service is reachable and healthy from external probes. It’s directly useful to monitor actual availability versus your SLO.

- Health checks, readiness, and liveness probes are internal to Kubernetes or Compute Engine — they don’t measure end-to-end availability from the user’s perspective.
    

---

### ✅ 3️⃣ **You've made a minor fix to one of your services. You want to deploy the new version with no downtime. Which would you choose?**

➡️ **Correct answer:**  
✔ **Rolling update**

**Explanation:**  
A **rolling update** gradually replaces old instances with new ones while keeping the service up. This avoids downtime during deployment.

- A/B and canary can help test changes but rolling update is the standard way to deploy **without downtime**.
    
- Blue/green also works but typically swaps environments all at once and might need traffic switching logic.
    

---

### ✅ 4️⃣ **You're deploying test environments using Compute Engine VMs. Some downtime is acceptable, and it is very important to deploy them as inexpensively as possible. What single thing below could save you the most money?**

➡️ **Correct answer:**  
✔ **Preemptible machines**

**Explanation:**  
**Preemptible VMs** are short-lived and can be shut down at any time — but they cost up to **80% less** than standard VMs. Perfect for test/dev where occasional interruptions are acceptable.  
Sustained use and committed use discounts save money too, but preemptibles save the most for workloads tolerant of disruption.