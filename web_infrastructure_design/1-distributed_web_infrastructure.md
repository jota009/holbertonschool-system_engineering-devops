```mermaid
graph TD
    A["User visits<br/>www.foobar.com"] --> B["DNS resolves to<br/>Load Balancer IP"]
    B --> C["HAproxy Load Balancer<br/>- Distributes traffic<br/>- Health checks servers<br/>- Single entry point"]

    C -->|"50% traffic"| D["Server 1"]
    C -->|"50% traffic"| E["Server 2"]

    subgraph D["SERVER 1"]
        D1["Nginx Web Server"]
        D2["Application Server"]
        D3["Application Files"]
        D4["MySQL Primary DB<br/>- Handles writes<br/>- Main database"]

        D1 --> D2
        D2 --> D3
        D3 --> D2
        D2 --> D4
        D4 --> D2
        D2 --> D1
    end

    subgraph E["SERVER 2"]
        E1["Nginx Web Server"]
        E2["Application Server"]
        E3["Application Files"]
        E4["MySQL Replica DB<br/>- Handles reads<br/>- Copy of primary"]

        E1 --> E2
        E2 --> E3
        E3 --> E2
        E2 --> E4
        E4 --> E2
        E2 --> E1
    end

    D4 -->|"Replication"| E4

    style C fill:#ffecb3
    style D fill:#e3f2fd
    style E fill:#e8f5e8
    style D4 fill:#ffcdd2
    style E4 fill:#c8e6c9
```
# 1. Distribited Web Infrastructure

## Components Added:
- 1 HAproxy Load Balancer
- 2 Servers (each with Ngnix, App
Server, App Files, MySQL)
- Primary-Replica database setup

## Why Each Addition:
- Load Balancer: Eliminates server SPOF, distributes traffic
- Second Server: Provides redundancy and scales capacity
- Database Replication: Separates reads/writes, improves performance

## Load Balancer Configuration:
- Algorithm: Round Robin (alternates requests between servers)
- Setup: Active-Active (both servers handle traffic simultaneously)

## Database Cluster:
- Primary: Handles all writes, replicates to Replica
- Replica: Handles reads, receives updates from Primary

## Issues:
- SPOF: Load Balancer Primary database
- Security: No firewall, no HTTPS encryption
- Operations: No monitoring system implemented
