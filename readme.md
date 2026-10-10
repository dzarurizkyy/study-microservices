# Study Microservices 🧩

This repository contains a comprehensive reference guide for Microservices architecture — covering monolith vs microservices trade-offs, data management, inter-service communication, and patterns such as API Gateway, CQRS, Service Discovery, and Centralized Configuration. The material is not tied to any specific technology stack.

## Installation 🔧

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/dzarurizkyy/study-microservices.git
   cd study-microservices
   ```

2. **Open the Guide**:
   - Read [Microservices Basics](001-microservice-basics.md) on GitHub, or open it in any Markdown viewer
   - Diagrams are stored in the `images/` folder and referenced from the guide

   > **Note:** No tools are required — the code snippets in the guide are illustrative sketches of each pattern, not a runnable project.

## List of Material 📚

- 🧩 **[Microservices Basics](001-microservice-basics.md)**

  Monolith vs microservices, database per service, NoSQL, RPI and messaging, orchestration and choreography, API Gateway, authentication, Backend for Frontend, CQRS, service discovery, service registry, and centralized configuration:

  ```text
  Client
    ↓
  API Gateway
    ├── User Service      → PostgreSQL
    ├── Product Service   → MongoDB
    ├── Payment Service   → PostgreSQL
    └── Notification Svc  (stateless)
  ```

  Services communicate through a message broker instead of calling each other directly:

  ```javascript
  // Producer: Order Service publishes an event
  await kafka.producer().send({
    topic: "order.created",
    messages: [{ value: JSON.stringify({ orderId: "123", userId: "456" }) }],
  });

  // Consumer: Notification Service subscribes independently
  await kafka.consumer().subscribe({ topic: "order.created" });
  ```

## 📍 References

- [Youtube](https://www.youtube.com/playlist?list=PL-CtdCApEFH-MtoBwQ0F3xNG21yjt5Kvs)

## 👨‍💻 Contributors

- [Dzaru Rizky Fathan Fortuna](https://www.linkedin.com/in/dzarurizky)
