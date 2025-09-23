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