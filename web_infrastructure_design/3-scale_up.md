```mermaid
graph TD
    A["User visits<br/>www.foobar.com"] -->
    B["DNS Load Balancer<br/>between HAproxy instances"]

    B --> C["HAproxy Load Balancer 1<br/>Primary LB"]
    B --> D["HAproxy Load Balancer 2<br/>Backup LB<br/>Cluster Configuration"]

    C <--> D

    C --> E["Web Server<br/>Dedicated Nginx Server"]
    D --> E

    E --> F["Application Server<br/>Dedicated App Logic Server"]

    F --> G["Database Server<br/>Dedicated MySQL Server"]

    subgraph E["WEB SERVER"]
        E1["Nginx Only<br/>- Serves static files<br/>- SSL termination<br/>- Reverse proxy"]
        E2["Monitoring Client"]
        E3["Firewall"]
    end

    subgraph F["APPLICATION SERVER"]
        F1["Application Runtime<br/>- Business logic only<br/>- Session management<br/>- API processing"]
        F2["Application Files<br/>- Your codebase<br/>- Business logic"]
        F3["Monitoring Client"]
        F4["Firewall"]

        F1 --> F2
        F2 --> F1
    end

    subgraph G["DATABASE SERVER"]
        G1["MySQL Database<br/>- Data storage only<br/>- Optimized for DB workloads<br/>- High RAM configuration"]
        G2["Monitoring Client"]
        G3["Firewall"]
    end

    style C fill:#ffecb3
    style D fill:#ffecb3
    style E fill:#e3f2fd
    style F fill:#f3e5f5
    style G fill:#e8f5e8
```
# 3. Scale Up Infrastructure

## Added Components:
- 1 Additional HAproxy Load Balancer (clustered configuration)
- 1 Dedicated Web Server (Nginx only)
- 1 Dedicated Application Server (business logic only)
- 1 Dedicated Databade Server (MySQL only)

## Why Each Addition:
- Second Load Balancer: Eliminates LB SPOF, enables maintenance without downtime
- Separated Components: Independent scaling, resource optimization, better performance

## Component Separation Benefits:
- Web Server: Optimized for static content, SSL termination, caching
- Application Server: Optimized for code execution, business logic processing
- Database Server: Optimized for data storage, query performance, high I/O

## Scaling Advantages:
- Independent Component scaling based on specific bottlenecks
- Resource optimization for eaxh workload type
- Easier troubleshooting and maintenance