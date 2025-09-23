# Scale up
## Final Infrastructure Design
````mermaid

sequenceDiagram
    participant U as User
    participant LB as HAProxy Cluster
    participant W as Web Tier
    participant A as App Tier
    participant DB as Data Base
    
    U->>LB: HTTPS Request
    LB->>W: Distribute to Web Server
    W->>A: Forward to App Server
    A->>DB: Read/Write Query
    DB->>A: Data Response
    A->>W: Rendered Content
    W->>LB: HTTP Response
    LB->>U: Final Response

````
### Components Added
- Additional server (3 total web servers)

- Load balancer cluster (active-active)

- Component separation by tier

### Tier Architecture
- Web Tier: Nginx servers (static content, SSL)

- Application Tier: Dedicated app servers (business logic)

- Database Tier: MySQL cluster (primary + replicas)

### Benefits
- Eliminated SPOFs: LB cluster, database redundancy

- Optimized Performance: Each tier specialized

- Independent Scaling: Scale tiers based on need

- Enhanced Security: Network segmentation

- Zero-downtime maintenance: Rolling updates possible

### Monitoring
- Comprehensive metrics from all tiers

- QPS tracking, performance alerts

- Health checks and automatic failover

### Evolution Summary
|Version	|Servers	|Key Features	|Limitations|
|-----------|-----------|---------------|-----------|
| 0. Simple	|1	|Basic LAMP stack|	Everything is SPOF|
|1. Distributed	|2	|Load balancing, DB replication|	No security, no monitoring|
|2. Secured	|2+DB	|HTTPS, firewalls, monitoring|	Poor |architecture, SSL termination issues|
|3. Scaled-Up|	6+	|Tiered architecture, clustering|	Production-ready|
### Key Concepts Explained
### Load Balancer Algorithms
- Round Robin: Sequential distribution to servers

- Active-Active: All servers handle traffic

- Active-Passive: Backup servers on standby

### Database Replication
- Primary: Handles writes, maintains binary log

- Replica: Copies changes, handles read queries

### SSL/TLS
- Termination at LB: Performance optimization but internal traffic unencrypted

- End-to-end encryption: More secure but higher resource usage

### Monitoring Metrics
- QPS (Queries Per Second): Web server request rate

- System metrics: CPU, memory, disk, network

- Application metrics: Error rates, response times

This infrastructure evolution demonstrates a complete journey from basic single-server setup to enterprise-grade, scalable, and secure web infrastructure.