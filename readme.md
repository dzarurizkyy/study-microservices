# Study Microservices 🧩

This repository contains a comprehensive reference guide for Microservices architecture, patterns, and best practices. It covers everything from monolith vs microservices tradeoffs to advanced patterns like CQRS, API Gateway, and Service Discovery.

## List of Material 📚

- 📘 **Monolith Architecture**

  A single deployable unit where all features — users, products, payments, notifications — are bundled together in one process and one database:

  ```
  Monolith App
  ├── UserModule
  ├── ProductModule
  ├── PaymentModule
  └── NotificationModule
       ↕ (one process, one database, one deployment)
  ```

- 📘 **Microservices Architecture**

  Small, independent services that each do one thing well and communicate via network calls:

  ```
  Client
    ↓
  API Gateway
    ├── User Service      → PostgreSQL
    ├── Product Service   → MongoDB
    ├── Payment Service   → PostgreSQL
    └── Notification Svc  (stateless)
  ```

- 📗 **Database per Service**

  Each service owns and manages its own database — no shared schema, no cross-service direct DB queries:

  ```yaml
  # docker-compose.yml
  services:
    user-db:
      image: postgres
      environment:
        POSTGRES_DB: user_db

    product-db:
      image: mongo

    payment-db:
      image: postgres
      environment:
        POSTGRES_DB: payment_db
  ```

- 📗 **Shared Database**

  A transitional pattern when migrating from monolith to microservices — multiple services temporarily share one database:

  ```
  User Service    ──┐
  Order Service   ──┼──→  Shared PostgreSQL DB
  Payment Service ──┘
  ```

- 📗 **NoSQL**

  Match the right database type to each service's access pattern:

  ```
  Document    → MongoDB           (flexible JSON-like records)
  Key-Value   → Redis             (fast caching, sessions)
  Column      → Apache Cassandra  (analytics, time-series)
  Search      → Elasticsearch     (full-text search, filtering)
  Graph       → Neo4j             (social networks, relationships)
  Time Series → InfluxDB          (metrics, logs, events)
  ```

- 📗 **Remote Procedure Invocation (RPI)**

  Synchronous inter-service communication — the caller waits for a response before continuing:

  ```javascript
  // Order Service calling Payment Service via REST
  const response = await fetch("http://payment-service/api/charge", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ orderId: "123", amount: 50000 }),
  });
  const result = await response.json();
  ```

- 📗 **Messaging**

  Asynchronous inter-service communication via a message broker — the sender does not wait for a reply:

  ```javascript
  // Producer: Order Service publishes an event
  await kafka.producer().send({
    topic: "order.created",
    messages: [{ value: JSON.stringify({ orderId: "123", userId: "456" }) }],
  });

  // Consumer: Notification Service subscribes independently
  await kafka.consumer().subscribe({ topic: "order.created" });
  ```

- 📙 **Types of Microservices**

  Three roles a microservice can play in a system:

  ```
  Stateless   → Currency Converter, Email Formatter (no DB, pure utility)
  Persistence → User Service, Product Service       (owns a DB, handles CRUD)
  Aggregation → Order Service                       (calls User + Product + Payment)
  ```

- 📙 **Service Orchestration**

  An Aggregation Service controls the full business flow via direct RPI calls — centralized logic, easy to trace:

  ```
  Order Service (Orchestrator)
    → calls User Service        (validate user)
    → calls Product Service     (check stock)
    → calls Payment Service     (charge card)
    → calls Notification Svc    (send receipt)
  ```

- 📙 **Service Choreography**

  Services react to events independently — no central coordinator, each service listens and acts on its own:

  ```
  Order Service → publishes [order.created] to Message Broker
                              ↓
          ┌───────────────────┼──────────────────┐
    Payment Svc         Product Svc        Notification Svc
    (subscribes)        (subscribes)        (subscribes)
  ```

- 📘 **API Gateway**

  A single entry point for all external traffic — acts as a reverse proxy, authentication middleware, and load balancer:

  ```nginx
  # Nginx as API Gateway
  server {
    location /api/users {
      proxy_pass http://user-service:3001;
    }
    location /api/products {
      proxy_pass http://product-service:3002;
    }
    location /api/orders {
      proxy_pass http://order-service:3003;
    }
  }
  ```

- 📘 **Authentication & Authorization**

  The Gateway validates JWT tokens and forwards the verified identity — downstream services skip re-validation:

  ```javascript
  // API Gateway validates JWT and forwards identity
  const decoded = jwt.verify(token, process.env.JWT_SECRET);

  req.headers["X-User-Id"] = decoded.userId;
  req.headers["X-User-Role"] = decoded.role;
  // Forward enriched request to downstream service
  ```

- 📙 **Backend for Frontend (BFF)**

  A dedicated backend per frontend type — each tailored to its client's authentication, bandwidth, and data shape needs:

  ```
  Mobile App  → Mobile BFF  → (compact payload, token-based auth)
  Web App     → Web BFF     → (full data, cookie-based auth)
  Smart TV    → TV BFF      → (minimal UI format, specific fields)
                  ↓
          Internal Microservices
  ```

- 📙 **CQRS (Command Query Responsibility Segregation)**

  Separate the write (Command) and read (Query) paths — each optimized with a different database:

  ```
  Write Path:
    POST /orders → Order Service → PostgreSQL (write-optimized)
                                      ↓ publishes event
  Read Path:
    GET  /orders → Query Service → Elasticsearch (read-optimized, fast search)
  ```

- 📗 **Server Side Discovery**

  A dedicated router sits in front of each service — clients only talk to the router, not individual instances:

  ```
  Client → Nginx (Router/Load Balancer) → payment-service:instance-1
                                        → payment-service:instance-2
                                        → payment-service:instance-3
  ```

- 📗 **Client Side Discovery**

  The calling service fetches live instance locations from a registry and performs its own load balancing:

  ```javascript
  // Fetch available instances from Service Registry
  const instances = await consul.catalog.service.nodes("payment-service");
  const target = instances[Math.floor(Math.random() * instances.length)];

  const response = await fetch(
    `http://${target.ServiceAddress}:${target.ServicePort}/charge`,
  );
  ```

- 📘 **Service Registry**

  Central directory of all running service instances — services register on startup, de-register on shutdown:

  ```bash
  # Register a service instance with Consul
  curl -X PUT http://consul:8500/v1/agent/service/register \
    -d '{
      "Name":    "payment-service",
      "Address": "10.0.0.5",
      "Port":    3003,
      "Check":   { "HTTP": "http://10.0.0.5:3003/health", "Interval": "10s" }
    }'
  ```

- 📘 **Centralized Configuration**

  All service configuration is stored in one dedicated service — change once, applied everywhere without redeployment:

  ```bash
  # Store config in Consul KV
  consul kv put config/payment-service/db_host  "db.internal"
  consul kv put config/payment-service/timeout  "30s"

  # Service fetches config on startup
  consul kv get config/payment-service/db_host
  ```

## 📍 References

- [Youtube](https://www.youtube.com/playlist?list=PL-CtdCApEFH-MtoBwQ0F3xNG21yjt5Kvs)

## 👨‍💻 Contributors

- [Dzaru Rizky Fathan Fortuna](https://www.linkedin.com/in/dzarurizky)
