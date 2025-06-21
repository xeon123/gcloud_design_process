These notes details Google Cloud’s networking capabilities, from global VPC design and load balancing to hybrid connectivity options like peering, VPN, and Cloud Interconnect. It provides tools (Network Intelligence Center, Cloud CDN) and frameworks to build reliable, performant networks, with hands-on activities to reinforce learning for real-world applications.

### Learning Objectives

- Design **VPC networks** to optimize cost, security, and performance.
- Configure **global and regional load balancers** for service access.
- Use **Cloud CDN** to reduce latency and egress costs.
- Evaluate network architecture with **Network Intelligence Center**.
- Connect networks via **peering**, **VPNs**, and **Cloud Interconnect**.

### Key Topics

1. **Designing Google Cloud Networks**:
    - **Global Network**: Google Cloud operates a worldwide network with regions (geographical locations), points of presence (PoPs), and a private fiber-optic network (including submarine cables) for high-bandwidth connectivity.
    - **VPC Networks**:
        - Global by default, with subnets created per region (auto or custom mode).
        - Resources across regions communicate via internal IPs without additional interconnects.
        - Custom subnets require non-overlapping IP ranges, support IP aliasing, and are expandable without downtime.
        - VMs can have up to 8 network interfaces, each connected to a different VPC (subnets must exist in the VM’s region).
    - **Shared VPC**:
        - Centralizes network management across multiple projects within an organization.
        - Hosted in one project, shared with service projects; admins control subnets, firewall rules, and routes, while developers focus on resource creation.
    - **Load Balancers**:
        - **Application Load Balancers** (Layer 7): Handle HTTP/HTTPS traffic, support SSL termination, session affinity, and content-based routing.
        - **Network Load Balancers** (Layer 4): Handle TCP/UDP traffic, ideal for low latency and high throughput.
        - Types include global/regional, external/internal, proxy/passthrough, with varying network service tiers (Premium/Standard).
        - Public-facing load balancers should use SSL (self-managed or Google-managed certificates).
    - **Cloud CDN**:
        - Enabled with global external Application Load Balancers to cache static content at edge locations, reducing latency and egress costs.
        - Supports content from Compute Engine, GKE, or Cloud Storage.
    - **Network Intelligence Center**:
        - Visualizes VPC topology and tests connectivity (e.g., between VPC endpoints, to/from the internet, or on-premises networks).
        - Useful for configuration validation and diagnostics.
2. **Connecting Networks**:
    - **VPC Peering**:
        - Connects two VPCs (same or different projects/organizations) for private RFC 1918 connectivity.
        - Requires non-overlapping subnet ranges and mutual approval by network admins.
    - **Cloud VPN**:
        - Securely connects on-premises networks to Google Cloud VPCs via IPsec tunnels over the public internet.
        - **Classic VPN**: 99.9% SLA, supports static/dynamic routes, single interface.
        - **HA VPN**: 99.99% SLA, requires dynamic (BGP) routing, dual interfaces, supports active/active or active/passive setups.
        - Topologies include HA VPN to peer devices, AWS virtual private gateways, or another HA VPN.
        - Max MTU: 1460 bytes due to encryption overhead.
    - **Cloud Interconnect**:
        - Provides dedicated, high-speed connections for on-premises to Google Cloud connectivity.
        - **Dedicated Interconnect**: Direct physical connection at colocation facilities (10–200 Gbps).
        - **Partner Interconnect**: Connection via a service provider (50 Mbps–10 Gbps).
        - Supports internal IP access to VPC resources and Private Google Access for Google services.
    - **Cloud Router**:
        - Enables dynamic route discovery (BGP) between connected networks, advertising local and peer routes.