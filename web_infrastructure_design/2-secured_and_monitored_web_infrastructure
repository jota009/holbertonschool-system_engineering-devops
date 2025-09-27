```mermaid
graph TD
    A["User visits<br/>www.foobar.com"] --> B["DNS resolves to<br/>Load Balancer IP"]
    B --> C["HTTPS Request<br/>Encrypted Traffic"]
    C --> D["Firewall 1<br/>- Filters malicious traffic<br/>- Port restrictions"]

    D --> E["HAproxy Load Balancer<br/>- SSL Certificate<br/>- SSL Termination<br/>- HTTPS to HTTP<br/>Monitoring Client 1"]

    E -->|"HTTP"| F["Firewall 2"]
    E -->|"HTTP"| G["Firewall 3"]

    F --> H["Server 1"]
    G --> I["Server 2"]

    subgraph H["SERVER 1"]
        H1["Nginx Web Server"]
        H2["Application Server"]
        H3["Application Files"]
        H4["MySQL Primary DB<br/>- Handles writes"]
        H5["Monitoring Client 2<br/>- Collects server metrics"]

        H1 --> H2
        H2 --> H3
        H3 --> H2
        H2 --> H4
        H4 --> H2
        H2 --> H1
    end

    subgraph I["SERVER 2"]
        I1["Nginx Web Server"]
        I2["Application Server"]
        I3["Application Files"]
        I4["MySQL Replica DB<br/>- Handles reads"]
        I5["Monitoring Client 3<br/>- Collects server metrics"]

        I1 --> I2
        I2 --> I3
        I3 --> I2
        I2 --> I4
        I4 --> I2
        I2 --> I1
    end

    H4 -->|"Replication"| I4

    H5 --> J["Monitoring Service<br/>Sumologic/Datadog/etc"]
    I5 --> J
    E --> J

    style D fill:#ffcccb
    style F fill:#ffcccb
    style G fill:#ffcccb
    style E fill:#fff3cd
    style H fill:#e3f2fd
    style I fill:#e8f5e8
    style J fill:#f3e5f5
```
# 2. Secured Web Infrastructure

## Added Security Components:
- 3 Firewalls (load balancer + 2 servers)
- 1 SSL Certificate (HEEPS encryption)
- 3 Monitoring clients (data collection)

## Components Purposes:
- Firewalls: Nertwork security, malicious traffic filtering
- SSL: Data encryption, user trust, compliance
- Monitoring: Performance tracking, proactive issue detection

## Monitoring Implementation:
- Agents collect system/app metrics every 60 seconds
- Data sent to centralized monitoring service
- QPS monitoring via Nginx status module + metric calculation

## Infrastucture Issues:
- SSL termination: Internal traffic unencrypted
- Single writer: MySQL Primary SPOF for writes
- Mixed components: Inefficient resource utilization, scaling limitations