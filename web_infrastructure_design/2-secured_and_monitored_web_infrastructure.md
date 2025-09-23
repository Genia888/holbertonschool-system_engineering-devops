# Secured and monitored web infrastructure
## Infrastructure Design
```mermaid

graph TB
    A[Users<br/>HTTPS: www.foobar.com] --> B[Firewall 1]
    B --> C[HAProxy + SSL Termination]
    
    C --> D[Firewall 2]
    C --> E[Firewall 3]
    
    D --> F[Server 1]
    E --> G[Server 2]
    
    subgraph F [Web Server 1]
        H[Nginx] --> I[App Server]
        I --> J[App Files]
        I --> K[MySQL Replica]
        L[Monitoring Client]
    end
    
    subgraph G [Web Server 2]
        M[Nginx] --> N[App Server]
        N --> O[App Files]
        N --> P[MySQL Replica]
        Q[Monitoring Client]
    end
    
    K --> R[MySQL Primary]
    P --> R
    
    subgraph R [Database Server]
        S[Firewall 4]
        S --> T[MySQL Primary]
        U[Monitoring Client]
    end

```
## Additional Components Explanation
### Why Each Element Was Added:
1. Three Firewalls
- Firewall 1: Protects load balancer from external attacks

- Firewall 2/3: Isolate web servers from internal threats

- Firewall 4: Protects database server with strict rules

- Purpose: Defense in depth strategy
2. SSL Certificate for HTTPS

- Purpose: Encrypts data between users and servers

- Benefit: Protects sensitive information and builds trust

- Implementation: Terminated at load balancer level

3. Three Monitoring Clients

- Purpose: Collect metrics from all critical components

- Benefit: Real-time visibility into system health

- Use: Performance tracking and alerting

### Why Traffic Served Over HTTPS?
HTTPS provides:

- Encryption: Prevents eavesdropping on sensitive data

- Data Integrity: Ensures data isn't modified in transit

- Authentication: Verifies server identity to prevent spoofing

- SEO Benefits: Google ranking preference for HTTPS sites

- User Trust: Browser padlock icon builds confidence

### What Monitoring is Used For?
Monitoring provides:

- Performance Tracking: CPU, memory, disk, network usage

- Availability Monitoring: Uptime/downtime tracking

- Security Monitoring: Detect suspicious activities

- Capacity Planning: Identify when to scale resources

- Troubleshooting: Quick identification of issues