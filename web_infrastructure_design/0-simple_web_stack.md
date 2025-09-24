```mermaid
graph TD
    A["User wants to visit<br/>www.foobar.com"] --> B["Browser asks DNS:<br/>What IP is www.foobar.com?"]
    B --> C["DNS Server responds:<br/>It is 8.8.8.8"]
    C --> D["Browser sends HTTP request<br/>to 8.8.8.8"]

    D --> E["SERVER: 8.8.8.8"]

    subgraph SERVER ["SERVER: 8.8.8.8"]
        F["Nginx Web Server<br/>- Receives HTTP requests<br/>- Serves static files<br/>- Forwards dynamic requests"]
        G["Application Server<br/>- Processes business logic<br/>- Executes application code<br/>- Handles user sessions"]
        I["Application Files<br/>- Your codebase PHP Python etc<br/>- Business logic files<br/>- Website functionality"]
        H["MySQL Database<br/>- Stores website data<br/>- User accounts posts etc"]

        F --> G
        G --> I
        I --> G
        G --> H
        H --> G
        G --> F
    end

    E --> K["Server sends HTML response<br/>back to browser"]
    K --> L["User sees website!"]

    style SERVER fill:#e1f5fe
    style F fill:#fff3e0
    style G fill:#f3e5f5
    style I fill:#fce4ec
    style H fill:#e8f5e8

```
## Infrastructure Components:
- 1 Server (IP: 8.8.8.8)
- Domain: foobar.com with www A record pointing to 8.8.8.8
- Nginx web server
- Application server
- MySQL database
- Application files (codebase)

## Request Flow:
1. User types www.foobar.com
2. DNS resolves to 8.8.8.8
3. HTTP request sent to server
4. Nginx receives request
5. Application server processes logic
6. MySQL provides data
7. Response sent back to user

## Infrastructure Issues:
- SPOF: Single server failure = complete outage
- Downtime during maintenance/deployments
- No horizontal scaling capability
- Limited by single server resources

