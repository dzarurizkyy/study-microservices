# 🧩 Microservices Basics

A practical reference guide for learning Microservices architecture from scratch — covering monolith vs microservices, data management, inter-service communication, API gateways, service discovery, and configuration.

---

## 📋 Table of Contents

- [Introduction](#-introduction)
  - [Who Is This For?](#who-is-this-for)
  - [What This Material Covers](#what-this-material-covers)
  - [Why Learn Microservices?](#why-learn-microservices)
- [Monolith Architecture](#️-monolith-architecture)
  - [What Is Monolith Architecture?](#what-is-monolith-architecture)
  - [Advantages of Monolith Architecture](#advantages-of-monolith-architecture)
  - [Problems with Monolith Architecture](#problems-with-monolith-architecture)
- [Microservices Architecture](#️-microservices-architecture)
  - [What Is Microservices Architecture?](#what-is-microservices-architecture)
  - [How Microservices Are Divided](#how-microservices-are-divided)
  - [Advantages of Microservices Architecture](#advantages-of-microservices-architecture)
  - [Problems with Microservices Architecture](#problems-with-microservices-architecture)
  - [How Small Should a Microservice Be?](#how-small-should-a-microservice-be)
  - [Monolith vs Microservices](#monolith-vs-microservices)
- [Database per Service](#️-database-per-service)
  - [Decentralized Database](#decentralized-database)
  - [Why Database per Service?](#why-database-per-service)
  - [Example: Database per Service](#example-database-per-service)
- [Shared Database](#-shared-database)
  - [What Is a Shared Database?](#what-is-a-shared-database)
  - [When to Use a Shared Database?](#when-to-use-a-shared-database)
  - [Example: Shared Database](#example-shared-database)
- [NoSQL](#-nosql)
  - [What Is NoSQL?](#what-is-nosql)
  - [Types of NoSQL Databases](#types-of-nosql-databases)
  - [Examples of NoSQL Databases](#examples-of-nosql-databases)
  - [Why Learn NoSQL?](#why-learn-nosql)
  - [NoSQL Case Study](#nosql-case-study)
- [Remote Procedure Invocation](#-remote-procedure-invocation)
  - [When a Service Needs Data from Another Service](#when-a-service-needs-data-from-another-service)
  - [Inter-Service Communication](#inter-service-communication)
  - [Examples of RPI Technologies](#examples-of-rpi-technologies)
  - [After Calling Another Service](#after-calling-another-service)
  - [Advantages of Using RPI](#advantages-of-using-rpi)
- [Messaging](#-messaging)
  - [When a Service Needs Data Asynchronously](#when-a-service-needs-data-asynchronously)
  - [Problems with RPI Communication](#problems-with-rpi-communication)
  - [Communication via Messaging](#communication-via-messaging)
  - [Examples of Message Brokers](#examples-of-message-brokers)
  - [Advantages of Using Messaging](#advantages-of-using-messaging)
- [Types of Microservices](#-types-of-microservices)
  - [Three Types of Microservices](#three-types-of-microservices)
  - [Stateless Microservices](#stateless-microservices)
  - [Persistence Microservices](#persistence-microservices)
  - [Aggregation Microservices](#aggregation-microservices)
  - [Microservices Types Case Study](#microservices-types-case-study)
- [Service Orchestration](#-service-orchestration)
  - [What Is Service Orchestration?](#what-is-service-orchestration)
  - [Advantages of Service Orchestration](#advantages-of-service-orchestration)
  - [Disadvantages of Service Orchestration](#disadvantages-of-service-orchestration)
- [Service Choreography](#-service-choreography)
  - [What Is Service Choreography?](#what-is-service-choreography)
  - [Advantages of Service Choreography](#advantages-of-service-choreography)
  - [Disadvantages of Service Choreography](#disadvantages-of-service-choreography)
  - [Orchestration vs Choreography](#orchestration-vs-choreography)
- [API Gateway](#-api-gateway)
  - [Exposing Microservices Without an API Gateway](#exposing-microservices-without-an-api-gateway)
  - [What Is an API Gateway?](#what-is-an-api-gateway)
  - [Advantages of API Gateway](#advantages-of-api-gateway)
  - [Examples of API Gateway](#examples-of-api-gateway)
- [Authentication & Authorization](#-authentication--authorization)
  - [Securing Microservices](#securing-microservices)
  - [Authentication](#authentication)
  - [Authorization](#authorization)
  - [Auth Service](#auth-service)
  - [Integration with Auth Service](#integration-with-auth-service)
  - [API Gateway as Auth Middleware](#api-gateway-as-auth-middleware)
  - [Supporting Technologies](#supporting-technologies)
- [Backend for Frontend](#-backend-for-frontend)
  - [The Problem with Many Frontend Types](#the-problem-with-many-frontend-types)
  - [What Is Backend for Frontend?](#what-is-backend-for-frontend)
  - [Advantages of BFF](#advantages-of-bff)
  - [GraphQL: An Alternative to BFF](#graphql-an-alternative-to-bff)
  - [Drawbacks of GraphQL](#drawbacks-of-graphql)
- [CQRS](#-cqrs-command-query-responsibility-segregation)
  - [Persistence Microservices Before CQRS](#persistence-microservices-before-cqrs)
  - [What Is CQRS?](#what-is-cqrs)
  - [CQRS Pattern](#cqrs-pattern)
  - [Advantages of CQRS](#advantages-of-cqrs)
  - [CQRS with Messaging](#cqrs-with-messaging)
  - [Advantages of CQRS with Messaging](#advantages-of-cqrs-with-messaging)
- [Server Side Discovery](#-server-side-discovery)
  - [Communication Between Microservices](#communication-between-microservices)
  - [What Is Server Side Discovery?](#what-is-server-side-discovery)
  - [Examples of Routers / Load Balancers](#examples-of-routers--load-balancers)
  - [Disadvantages of Server Side Discovery](#disadvantages-of-server-side-discovery)
- [Client Side Discovery](#-client-side-discovery)
  - [What Is Client Side Discovery?](#what-is-client-side-discovery)
  - [Disadvantages of Client Side Discovery](#disadvantages-of-client-side-discovery)
- [Service Registry](#-service-registry)
  - [What Is a Service Registry?](#what-is-a-service-registry)
  - [Registering with the Service Registry](#registering-with-the-service-registry)
  - [Querying the Service Registry](#querying-the-service-registry)
  - [Health Check in the Service Registry](#health-check-in-the-service-registry)
  - [Examples of Service Registry Applications](#examples-of-service-registry-applications)
- [Centralized Configuration](#️-centralized-configuration)
  - [Where to Store Configuration?](#where-to-store-configuration)
  - [What Is Centralized Configuration?](#what-is-centralized-configuration)
  - [Getting Configuration](#getting-configuration)
  - [Examples of Centralized Configuration Applications](#examples-of-centralized-configuration-applications)
- [Quick Reference](#-quick-reference)
- [Best Practices](#-best-practices)

---

## 🎯 Introduction

### Who Is This For?

- **Web Programmer** — Understands how the frontend integrates with multiple backend services
- **Backend Programmer** — Learns how to design and maintain independently deployable services
- **Software Architect** — Gains the tools to design scalable, distributed system architectures
- **DevOps Engineer** — Understands the deployment, scaling, and operational needs of microservices

### What This Material Covers

- Theory and concepts behind microservices
- Real-world case studies
- Not tied to any specific technology stack

### Why Learn Microservices?

- **Industry standard** — Core knowledge in modern tech companies
- **Rich ecosystem** — Plenty of supporting tools, patterns, and platforms
- **Proven at scale** — Widely adopted by leading tech companies, especially at scale
- **Career growth** — Required knowledge for Senior Engineers

---

## 🏛️ Monolith Architecture

> **Analogy:** Think of a traditional restaurant where one big kitchen handles everything — cooking, frying, making drinks — all in the same place. If the stove breaks, the entire restaurant shuts down. Everyone depends on the same kitchen, the same equipment, the same staff.

### What Is Monolith Architecture?

![Monolith Architecture](images/001.png)

A monolith is an application where all features — user management, product catalog, payments, notifications — are built and bundled together into a single deployable unit.

> **Tip:** Start with a monolith. For a new project, a monolith is often the right starting point — it's simple, fast to build, and easy to understand.

### Advantages of Monolith Architecture

- **Easy to develop** — Everything is in one place; no inter-service communication to manage
- **Easy to deploy** — A single artifact to build and ship
- **Easy to test** — End-to-end tests run in one process
- **Easy to scale** — Deploy more copies of the entire application

### Problems with Monolith Architecture

- **Intimidating for new developers** — The entire codebase must be understood before contributing
- **Scaling development with many engineers is difficult** — Merge conflicts, slow CI, team coordination overhead
- **Long-term technology lock-in** — Tightly coupled to a single language, database, and framework
- **Cannot scale specific parts** — The entire application must be scaled even if only one feature is under load
- **Heavy to run locally** — The full app must start even for small changes

---

## ⚙️ Microservices Architecture

> **Analogy:** A modern food court instead of one big kitchen. Each stall (service) specializes in one thing — one for drinks, one for main courses, one for desserts. If the drinks stall has a problem, the food stalls keep running. Each stall can expand or replace its equipment independently.

### What Is Microservices Architecture?

![Microservices Architecture](images/002.png)

- Small, focused applications that work together
- Each service does **one thing well**
- **Independent** — can be deployed and changed without depending on other services
- Each component in the system is a separate service
- Services communicate with each other via **network calls**

### How Microservices Are Divided

![Division of Microservices](images/003.png)

### Advantages of Microservices Architecture

- **Easy to understand** — Each service is small and focused
- **Easier to develop, maintain, test, and deploy** — Independent lifecycles per service
- **Technology flexibility** — Each service can use the best tool for its job
- **Independent scaling** — Scale only the services that need more resources
- **Small team ownership** — Each service can be owned and operated by a small team

### Problems with Microservices Architecture

- **Distributed system complexity** — Network failures, latency, and partial failures become real concerns
- **Inter-service communication is error-prone** — The network is not reliable
- **Integration testing is harder** — Testing the interactions between services requires more setup

> **Key Insight:** Microservices trade code complexity for operational complexity. Every function call that used to happen in memory now crosses the network — and the network can fail.

### How Small Should a Microservice Be?

- **Single Responsibility** — Each service does one thing well
- **Understandable by one person** — Small enough that a single developer can hold it in their head
- **Buildable by a small team** — Commonly referenced as the "two-pizza team" rule

### Monolith vs Microservices

| Monolith | Microservices |
| --- | --- |
| Simplicity | Partial Deployment |
| Consistency | High Availability |
| Easy to Refactor | Multiple Platform Support |
| — | Easy to Scale |

---

## 🗄️ Database per Service

> **Analogy:** Each restaurant stall owns its own kitchen storage. The drinks stall stores its own syrup and ice; the food stall stores its own ingredients. No stall can walk into another's storage without permission. This keeps things clean, independent, and prevents one messy stall from affecting the others.

### Decentralized Database

![Decentralized Database](images/004.png)

### Why Database per Service?

- **Ensures independence** — Services are not coupled through a shared database schema
- **Technology freedom** — Each service can use the database type best suited to its needs (SQL, document, key-value, etc.)
- **Encapsulation** — A service never needs to know the internal data structure of another service

### Example: Database per Service

![Database per Service Example](images/005.png)

---

## 🔗 Shared Database

> **Analogy:** During a transition period, multiple stalls temporarily share one central storage room. It's not ideal — stalls can accidentally see or touch each other's ingredients — but it's a pragmatic shortcut while the proper separation is being set up.

### What Is a Shared Database?

![Shared Database](images/006.png)

### When to Use a Shared Database?

- When **transitioning** from a monolith to microservices — splitting everything at once is risky
- When you're **unsure how to partition** the data between services
- When there's a **tight deadline** and no time to build proper APIs between services

> **Gotcha:** A shared database is a temporary bridge, not a destination. As long as services share tables, a schema change in one service can silently break another.

### Example: Shared Database

![Shared Database Example](images/007.png)

---

## 📊 NoSQL

> **Analogy:** Not all storage needs the same kind of shelf. A library uses bookshelves sorted by category. A warehouse uses racks sorted by size and weight. A photo studio uses flat filing cabinets. NoSQL is a family of different storage solutions, each designed for a different kind of data problem.

### What Is NoSQL?

- NoSQL does **not** mean "NO SQL"
- NoSQL stands for **Not Only SQL** — it extends beyond the relational model

### Types of NoSQL Databases

| Type | Description |
| --- | --- |
| **Document Oriented** | Stores data as flexible JSON-like documents |
| **Key-Value** | Simple key → value lookups; extremely fast |
| **Column Families** | Stores data in columns rather than rows; great for analytics |
| **Graph** | Stores nodes and relationships; great for social networks |
| **Search** | Optimized for full-text search and filtering |
| **Time Series** | Optimized for time-stamped data (metrics, logs, events) |

### Examples of NoSQL Databases

| Database | Type |
| --- | --- |
| **MongoDB** | Document Oriented |
| **Elasticsearch** | Search |
| **Redis** | Key-Value |
| **Apache Cassandra** | Column Families |
| **Neo4J** | Graph |
| **InfluxDB** | Time Series |

### Why Learn NoSQL?

- **Match the right tool to the problem** — Not every problem fits a relational table
- **Find alternative data processing strategies** — Document, graph, and time-series models solve different problems
- **Improve performance** — Using the right database type speeds up both writes and reads

### NoSQL Case Study

![NoSQL Case Study](images/008.png)

---

## 🔄 Remote Procedure Invocation

> **Analogy:** When one stall needs an ingredient from another, they pick up the phone and call directly. "Do you have any syrup?" — "Yes, I'll send it over." It's synchronous: you wait on the line until you get the answer. It's simple, direct, and straightforward for most requests.

### When a Service Needs Data from Another Service

![Service Needs Data](images/009.png)

### Inter-Service Communication

- Ideally done via **RPI (Remote Procedure Invocation)** or **RPC (Remote Procedure Call)**
- **Not recommended** to communicate via a shared database

### Examples of RPI Technologies

- RESTful API (HTTP)
- gRPC
- Apache Thrift
- SOAP
- Java RMI
- CORBA (Common Object Request Broker Architecture)

### After Calling Another Service

![Service After RPI](images/010.png)

### Advantages of Using RPI

- **Simple and straightforward** — Easy to implement and reason about
- **Request-Reply pattern** — Natural fit for synchronous workflows
- **Synchronous** — The caller waits for a response, making the flow easy to trace

---

## 📨 Messaging

> **Analogy:** Instead of calling each stall one by one, the head kitchen posts an announcement on a bulletin board (message broker): "Order #42 has been placed." Every stall that cares about orders checks the board and handles its own part — the grill station starts cooking, the drinks station starts preparing, the packaging station gets ready — all in parallel, without waiting for each other.

### When a Service Needs Data Asynchronously

![Messaging Flow](images/011.png)

### Problems with RPI Communication

![RPI Communication Problems](images/012.png)

- **Slow for long-running tasks** — Email and SMS services may take time; the caller is blocked waiting
- **Sending the same data multiple times** — Finance and Report services both need the same event
- **Parallel processing is complex** — Coordinating multiple downstream services from one caller is hard

### Communication via Messaging

- Used for **asynchronous** communication — fire and forget
- The sender does **not need to wait** for a response from the receiver
- Sometimes the sender doesn't care about a reply at all
- Requires a **Message Channel** as the bridge between sender and receiver
- Recommended to use a **Message Broker** application to manage channels

### Examples of Message Brokers

- Redis (PubSub)
- Apache Kafka
- RabbitMQ
- NSQ
- Google Pub/Sub
- Amazon SQS

### Advantages of Using Messaging

![Messaging Advantages](images/013.png)

- **Faster** — The sender doesn't wait for the receiver to finish processing
- **Decoupled** — The sender doesn't need to know or care about who receives the message

> **Note:** RPI and Messaging are not mutually exclusive. Use RPI when the caller needs the result right now to continue, and Messaging when the work can happen in the background or must reach several consumers.

---

## 🧩 Types of Microservices

> **Analogy:** In a food court, not all stalls play the same role. Some just prepare ingredients (stateless utility). Some own and manage the pantry (persistence). Some act as the head coordinator, combining work from multiple stalls before delivering to the customer (aggregation).

### Three Types of Microservices

| Type | Description |
| --- | --- |
| **Stateless** | No database; does one simple, self-contained task |
| **Persistence** | Has its own database; manages CRUD operations for a domain |
| **Aggregation** | Depends on other services; orchestrates business logic |

### Stateless Microservices

- Usually has **no database**
- Used for **simple, self-contained tasks**
- Acts as a **utility** for other microservices
- **Does not depend** on other microservices

![Stateless Microservice Example](images/014.png)

### Persistence Microservices

- Usually has **its own database**
- Also known as a **Master Data Microservice**
- Handles **CRUD operations** for its domain

![Persistence Microservice Example](images/015.png)

### Aggregation Microservices

- **Depends on** other microservices
- Acts as the **center of business logic** for a feature or flow
- **May or may not** have its own database
- **Cannot stand alone** — requires other services to function

![Aggregation Microservice Example](images/016.png)

### Microservices Types Case Study

![Microservices Type Case Study](images/017.png)

---

## 🎼 Service Orchestration

> **Analogy:** A conductor stands in front of the orchestra and tells every musician exactly when to play. The conductor knows the entire score and gives explicit instructions: "Strings first, then brass, then drums." Without the conductor, the musicians don't know when to start. The conductor is the single point of knowledge and control.

### What Is Service Orchestration?

- When an **Aggregation Microservice** communicates with other services via **RPI (Remote Procedure Invocation)**, that pattern is called **Service Orchestration**
- The Aggregation Microservice is responsible for **orchestrating the entire business logic flow**
- It calls other services directly and waits for their responses

![Service Orchestration Example](images/018.png)

### Advantages of Service Orchestration

- **Easy to build** — Business logic is centralized in one place
- **Easy to understand** — The entire flow can be traced by reading one service

### Disadvantages of Service Orchestration

- **Tight coupling** — The Aggregation service depends heavily on all downstream services
- **Slower** — Must wait for each downstream service to respond
- **More fragile** — If any downstream service has a problem, the Aggregation service fails too
- **Requires changes for new services** — Adding a new downstream step means modifying the Aggregation service

![Service Orchestration Drawback](images/019.png)

---

## 💃 Service Choreography

> **Analogy:** Instead of a conductor, imagine a dance performance where every dancer has memorized their own routine and listens for music cues. When the beat drops, each dancer knows exactly what to do — no one is being directed in real time. The performance emerges from all dancers independently responding to the same shared rhythm (the message broker).

### What Is Service Choreography?

- Different from Orchestration — uses **Messaging** instead of direct RPI calls
- In Orchestration, the Aggregation service knows and controls everything
- In Choreography, **every service is smart** — each listens for events and reacts independently
- No single service holds all the knowledge of the full flow

![Service Choreography Example](images/020.png)

### Advantages of Service Choreography

![Service Choreography Advantages](images/021.png)

- **Aggregation service is decoupled** — It only publishes events; it doesn't know who consumes them
- **Faster** — No waiting for downstream services to respond synchronously
- **Adding new services is easy** — New consumers just subscribe to existing events; the publisher doesn't change

### Disadvantages of Service Choreography

- **Harder to debug** — When something goes wrong, tracing the full flow requires checking multiple services and the message broker
- **Business logic is distributed** — The overall flow is spread across many services, making it hard to understand at a glance

### Orchestration vs Choreography

| | Orchestration | Choreography |
| --- | --- | --- |
| Communication | RPI (synchronous) | Messaging (asynchronous) |
| Business logic | Centralized in the Aggregation service | Distributed across services |
| Coupling | Tight | Loose |
| Debugging | Easy — read one service | Harder — trace events across services |
| Adding a new step | Modify the Aggregation service | Subscribe a new consumer |
| Best for | Simple, linear flows owned by one team | Parallel, event-driven flows owned by many teams |

---

## 🚪 API Gateway

> **Analogy:** A shopping mall has one main entrance. You don't enter each store through its own back door on a dark alley. At the front entrance, there are security guards, a directory, and a visitor log. All visitors go through one controlled door — and everything behind it stays protected.

### Exposing Microservices Without an API Gateway

![Exposing Microservices Problem](images/022.png)

- **All services are accessible from the internet** — Every service is a potential attack surface
- **Authentication must be implemented in every service** — Duplicated effort and inconsistent enforcement
- **Data leakage risk** — Internal service errors and structure are exposed directly to clients

### What Is an API Gateway?

![API Gateway](images/023.png)

- The API Gateway is the **single entry point** from the outside world into the microservices system
- "Outside" = internet traffic; "Inside" = your microservices
- Acts as a **proxy server** to all microservices — clients only talk to the gateway
- Microservices are **not directly accessible** from the internet

### Advantages of API Gateway

- **More secure** — Single controlled entry point
- **Centralized authentication** — Services don't need to implement auth; it's handled at the gateway
- **Load balancing** — Can distribute traffic across service instances
- **Rate limiting** — Protects services from being overwhelmed
- **Error shielding** — Internal service errors are not exposed to clients

> **Gotcha:** Because every request passes through it, the API Gateway becomes a single point of failure. Always run it as multiple instances behind a load balancer.

### Examples of API Gateway

- Nginx
- Apache HTTPD
- Kong
- Netflix Zuul
- Spring Cloud Gateway

---

## 🔐 Authentication & Authorization

> **Analogy:** A concert venue has two checkpoints. The first is the ticket scanner at the gate — it verifies you are who you say you are (Authentication). The second is the section usher — it checks whether your ticket allows you into the VIP section or just general admission (Authorization). Passing the gate doesn't automatically grant access everywhere inside.

### Securing Microservices

![Securing Microservices](images/024.png)

### Authentication

- Validates credentials to **verify the identity** of a caller
- Examples: username/password login, OAuth token, API key, biometrics

### Authorization

- Performed **after** authentication
- Validates whether the verified identity has **permission to access** the requested resource
- Examples: Access Control Lists (ACL), Role-Based Access Control (RBAC)

| | Authentication | Authorization |
| --- | --- | --- |
| Question answered | *Who are you?* | *What are you allowed to do?* |
| Order | First | After authentication |
| Examples | Login, OAuth token, API key | ACL, RBAC |

### Auth Service

![Auth Service](images/025.png)

### Integration with Auth Service

![Auth Service Integration](images/026.png)

### API Gateway as Auth Middleware

![API Gateway as Middleware](images/027.png)

### Supporting Technologies

- Secure Cookie
- OAuth
- JSON Web Token (JWT)
- Basic Auth
- API Key / Secret Key

---

## 📱 Backend for Frontend

> **Analogy:** A restaurant that serves both dine-in customers and delivery riders doesn't use the same counter for both. The dine-in counter is designed for sit-down orders; the delivery window is optimized for fast handoff. Each frontend (channel) has a backend tailored to exactly what it needs.

### The Problem with Many Frontend Types

![Multiple Frontend Problem](images/028.png)

- Each frontend has **different authentication mechanisms** (web session vs. mobile token vs. smart TV)
- **Bandwidth varies** — a mobile app needs lightweight responses; a desktop web app can handle more
- **Required API shape differs** — mobile apps need compact, aggregated responses; desktop can make more granular calls
- **A single API Gateway must serve all needs** — leading to bloated, compromised APIs

### What Is Backend for Frontend?

![Backend for Frontend](images/029.png)

- BFF provides a **dedicated backend for each specific frontend**
- One backend per frontend type — mobile BFF, web BFF, TV BFF
- The more frontend types, the more BFFs are created
- Each BFF can be owned and iterated on independently by the corresponding frontend team

### Advantages of BFF

- **Isolated development** — Each frontend's backend is developed separately without affecting others
- **Clean separation of concerns** — Frontend-specific logic doesn't pollute a shared backend layer

### GraphQL: An Alternative to BFF

![GraphQL as BFF Alternative](images/030.png)

- GraphQL is a **query language for APIs**
- Allows the frontend to **manipulate the response shape at runtime**
- The frontend decides exactly what data it wants — the backend provides a complete graph and the client selects what it needs

### Drawbacks of GraphQL

- Requires building a **GraphQL Server** on the backend
- Requires building a **GraphQL Client** on the frontend

---

## ⚡ CQRS (Command Query Responsibility Segregation)

> **Analogy:** A library separates its operations into two departments: the "Write" desk for returning and adding new books (commands), and the "Search" desk for finding books (queries). The search desk uses a fast digital catalog optimized for searching. The write desk updates the master ledger. They use different tools because their jobs are fundamentally different.

### Persistence Microservices Before CQRS

![Persistence Microservice CQRS](images/031.png)

### What Is CQRS?

- CQRS separates **Command operations** from **Query operations**
- **Command** — operations that **change data** (Create, Update, Delete)
- **Query** — operations that **read data** (Get, Search)
- In CQRS, the service and/or database is split: one side for commands, one side for queries

### CQRS Pattern

![CQRS Pattern](images/032.png)

### Advantages of CQRS

- **Optimal databases for each operation** — Use a write-optimized database for commands, a read-optimized database (e.g., Elasticsearch) for queries
- **Cleaner models** — Command and query models are separate; no single model trying to serve both
- **Better overall performance** — Read and write paths are independently optimized

### CQRS with Messaging

![CQRS with Messaging](images/033.png)

### Advantages of CQRS with Messaging

- **Parallel development** — Command and Query applications can be built by separate teams simultaneously
- **Decoupled data flow** — The Command app only needs to publish events to the broker; it doesn't need to know the Query app's data structure
- **Independent scaling** — Scale the read side or write side based on actual load
- **Resilience** — If the Query app is down, events stay safely in the broker and are processed when it recovers
- **Easier retry** — Message brokers provide built-in retry and dead-letter mechanisms

> **Gotcha:** With CQRS over messaging, the query side is **eventually consistent** — a record written through the command side may not appear in search results for a short moment.

---

## 🔃 Server Side Discovery

> **Analogy:** Every team in an office building gets a shared receptionist outside their room. When a visitor wants to reach "Team A," they just go to Team A's receptionist, who knows which desks are available and routes the visitor accordingly. The visitor never needs to know how many desks are inside.

### Communication Between Microservices

![Communication Between Microservices](images/034.png)

### What Is Server Side Discovery?

- A **dedicated router or load balancer** sits in front of each service
- The client only connects to the **router** — it doesn't need to know about individual service instances
- When instances are added or removed, **only the router changes** — the client stays untouched

![Server Side Discovery](images/035.png)

### Examples of Routers / Load Balancers

- Nginx
- Apache HTTPD
- Traefik

### Disadvantages of Server Side Discovery

![Server Side Discovery Drawback](images/036.png)

- **Every service needs its own router** — Operational overhead multiplies with service count
- **To avoid a single point of failure**, each router must run as **at least 2 instances**
- **Higher cost** — Every service requires 2 router instances running at all times

---

## 🔍 Client Side Discovery

> **Analogy:** Instead of a receptionist, each visitor carries a personal directory book that lists all the desks in every room. When they need to visit Team A, they look it up themselves and walk directly to the right desk. Faster access — but now the visitor is responsible for keeping their directory book up to date.

### What Is Client Side Discovery?

- The **client itself is responsible** for knowing the location of all service instances
- **No router or load balancer** needed between services
- All load distribution logic is handled by the **client / calling service**

![Client Side Discovery](images/037.png)

### Disadvantages of Client Side Discovery

- **Client must know all service locations** — Tightly coupled to deployment topology
- **When instances are added or removed**, the client must be updated with the new locations
- **If the client implements load balancing incorrectly**, traffic to target services may be uneven

> **Note:** These drawbacks are exactly what a [Service Registry](#-service-registry) solves — the client looks up locations from the registry instead of hard-coding them.

---

## 📋 Service Registry

> **Analogy:** A central company directory on the intranet. When a new employee joins, they register themselves: "My name is Bob, I'm in Room 412." When they leave, they de-register. When another employee needs Bob, they look him up in the directory — and the directory guarantees that Bob is actually reachable, because it performs regular health checks.

### What Is a Service Registry?

- An application used as a **central store of all service location information**
- Every service **registers its address** when it starts up
- Every service **de-registers** when it shuts down, so the registry stops routing traffic to it

### Registering with the Service Registry

![Registering with Service Registry](images/038.png)

### Querying the Service Registry

![Querying Service Registry](images/039.png)

### Health Check in the Service Registry

![Health Check in Service Registry](images/040.png)

### Examples of Service Registry Applications

- [Hashicorp Consul](https://www.consul.io/)
- [Netflix Eureka](https://github.com/Netflix/eureka)

---

## ⚙️ Centralized Configuration

> **Analogy:** Instead of every employee keeping a personal notebook of office rules and passwords, the company maintains one official intranet page with all the settings. When a rule changes, the intranet page is updated once — and everyone who reads it gets the new value automatically. No more "my copy says X, your copy says Y."

### Where to Store Configuration?

Every application has configuration — database credentials, feature flags, timeouts, API endpoints. The question is: where should it live so it's easy to maintain and consume?

| Location | Trade-offs |
| --- | --- |
| **Database** | Persistent and queryable, but adds a DB dependency for startup |
| **File** | Simple and familiar, but hard to share across many service instances |
| **Environment Variable** | Lightweight and container-friendly, but managed per instance |

### What Is Centralized Configuration?

- A pattern where **all configuration is stored in a dedicated service**
- Services that need configuration **pull it from this central service** at startup or runtime
- Changing a value in one place is reflected in all services without redeployment

### Getting Configuration

![Centralized Configuration](images/041.png)

### Examples of Centralized Configuration Applications

- [Hashicorp Consul](https://www.consul.io/)
- [Hashicorp Vault](https://www.vaultproject.io/)
- [Etcd](https://etcd.io/)
- [Apache Zookeeper](https://zookeeper.apache.org/)
- [Doozerd](https://github.com/ha/doozerd)

---

## 🎯 Quick Reference

| Pattern | Problem Solved | Key Trade-off |
| --- | --- | --- |
| **Database per Service** | Decouples data ownership between services | Each service manages its own schema and migrations |
| **Shared Database** | Speeds up monolith-to-microservices transition | Services remain coupled through the database schema |
| **NoSQL** | Matches data storage to access patterns | More operational complexity; no universal query language |
| **RPI / REST / gRPC** | Simple synchronous service-to-service calls | Caller is blocked waiting; downstream failures cascade |
| **Messaging** | Async, decoupled inter-service communication | Harder to trace and debug distributed flows |
| **Stateless Microservice** | Lightweight utility with no persistence | Cannot store state; must rely on other services for data |
| **Persistence Microservice** | Owns and manages a data domain | Must expose APIs; no direct DB access from other services |
| **Aggregation Microservice** | Coordinates business logic across services | Depends on multiple services; must handle partial failures |
| **Service Orchestration** | Centralized, easy-to-read business flow | Tight coupling; single point of failure for the flow |
| **Service Choreography** | Loose coupling via event-driven communication | Business logic is distributed and harder to trace |
| **API Gateway** | Single entry point for all client traffic | Potential bottleneck; must be highly available |
| **Backend for Frontend** | Tailored APIs per frontend type | More services to build and maintain |
| **GraphQL** | Flexible, runtime-shaped API responses | Additional GraphQL server and client complexity |
| **CQRS** | Separate read and write optimization | Eventual consistency between command and query sides |
| **Server Side Discovery** | Clients don't need to know service locations | Router per service doubles infrastructure cost |
| **Client Side Discovery** | No extra router infrastructure needed | Client logic must track and update service locations |
| **Service Registry** | Central source of truth for service locations | Registry itself must be highly available |
| **Centralized Configuration** | One place to manage all service config | Config service must be highly available at startup |

---

## 💡 Best Practices

**✅ Do This**

- **Start with a monolith, migrate incrementally** — understand your domain boundaries before splitting them into services
- **Use a Shared Database only as a temporary bridge** during the monolith-to-microservices migration
- **Use the right database for each service** — a relational DB for transactional data, Elasticsearch for search, Redis for caching
- **Prefer Messaging for long-running or broadcast operations** — if the caller doesn't need an immediate response, publish to a message broker
- **Use RPI only when the result is needed synchronously** to continue processing
- **Always put an API Gateway in front of your services** — centralize authentication, rate limiting, and logging in one place
- **Use JWT for stateless authentication across services** — the gateway validates the token and downstream services trust the forwarded identity, without calling the Auth Service on every request
- **Choose Orchestration or Choreography consciously** — see [Orchestration vs Choreography](#orchestration-vs-choreography)
- **Implement health checks and graceful shutdown** — register with the Service Registry on startup and de-register on shutdown
- **Centralize configuration, externalize secrets** — a configuration service for non-sensitive settings, a secrets manager (Vault, AWS Secrets Manager) for credentials
- **Design for failure** — every network call can fail, so implement timeouts, retries, and circuit breakers
- **Use the Bulkhead pattern** to prevent one slow service from exhausting all connection pools

**❌ Avoid This**

- **Going microservices from day one** — splitting before the domain is understood produces the wrong service boundaries
- **Querying another service's database directly** — always go through that service's API
- **Using RPI for broadcast events** — calling every interested service one by one couples the caller to all of them
- **Exposing microservices directly to the public internet** — every exposed service is an attack surface
- **Skipping de-registration on shutdown** — other services may keep routing traffic to dead instances
- **Committing secrets to code** — credentials belong in a secrets manager, never in the repository
- **Assuming the network is reliable** — a call without a timeout can hang a whole chain of services

> Reference: [microservices.io — Pattern Language](https://microservices.io/patterns/) · [Martin Fowler — Microservices](https://martinfowler.com/articles/microservices.html)
