## Key Topics

These notes teaches how to gather and define service requirements, understand users through roles and personas, and measure success with KPIs, SLIs, SLOs, and SLAs. It provides a structured approach for cloud architects to design systems that meet both business and technical needs while ensuring user satisfaction and operational efficiency.

### Learning Objectives:

- Describe users via roles and personas.
- Write qualitative requirements as user stories.
- Define quantitative requirements using KPIs.
- Apply SMART criteria to evaluate requirements.
- Set appropriate SLOs and SLIs for services.

### Requirements, Analysis, and Design

- **Qualitative Requirements**: Defined from the user's perspective, addressing "who" (users, developers, stakeholders), "what" (main features), "why" (purpose), "when" (timeline), and "how" (non-functional requirements like scalability or latency).
- **User Roles**: Represent user goals (e.g., shopper, administrator), not job titles. Roles are identified through brainstorming, organizing, consolidating, and refining.
- **Personas**: Fictional representations of users to understand their characteristics and needs (e.g., Jocelyn, a busy mom managing bank accounts online).
- **User Stories**: Describe features from a user’s viewpoint using the format "As a [role], I want to [action], so that [benefit]" (e.g., "As an account holder, I want to check my balance anytime to avoid overdrawing"). Stories should follow the INVEST criteria (Independent, Negotiable, Valuable, Estimatable, Small, Testable).
- **Activity 2**: Involves refining roles, writing personas, and creating user stories for a case study (e.g., an online store or travel portal).

### Quantitative Requirements

- Measurable aspects like time, finance, and user scale, constrained by resources (time, funding, people).
- **Key Performance Indicators (KPIs)**: Metrics to measure success, divided into business KPIs (e.g., ROI, customer churn) and technical KPIs (e.g., page views, checkouts). KPIs should align with goals (e.g., increasing online store turnover by tracking conversion rates) and follow SMART criteria (Specific, Measurable, Achievable, Relevant, Time-bound).

### Service Level Indicators (SLIs), Objectives (SLOs), and Agreements (SLAs)

- **SLIs**: Quantitative measures of service performance (e.g., latency, error rate, throughput). Must be measurable and time-bound (e.g., "HTTP GET requests respond within 400 ms aggregated per minute").
- **SLOs**: Targets for SLIs (e.g., "99% of HTTP responses ≤ 200 ms"). Should be achievable, relevant, and not overly ambitious to avoid high costs.
- **SLAs**: Contracts with customers specifying penalties for failing to meet thresholds, which are less strict than SLOs (e.g., compensation if 99th percentile latency exceeds 300 ms).
- **Activity 3**: Involves defining SLIs and SLOs for case study features (e.g., 99.95% availability for an online store’s search service).
- **Examples**: For a travel portal, SLIs include HTTP response fractions or query times, with SLOs like 99.95% availability or 95% of requests under 200 ms.


