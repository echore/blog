---
share: true
---

2026-03-07  14:45
Tags: [[Technical Literacy|Technical Literacy]]


https://www.redhat.com/en/topics/api/what-are-application-programming-interfaces

The 2 architectural approaches that use remote APIs most are [service-oriented architecture (SOA)](https://www.redhat.com/en/topics/cloud-native-apps/what-is-service-oriented-architecture) and microservices architecture. SOA, the oldest of the 2 approaches, began as an improvement to monolithic apps. Whereas a single monolithic app does everything, some functions can be supplied by different apps that are loosely coupled through an integration pattern, like an enterprise service bus (ESB).

While SOA is, in most respects, simpler than a monolithic architecture, it carries a risk of cascading changes throughout the environment if component interactions are not clearly understood. This additional complexity reintroduces some of the problems SOA sought to remedy.

Microservices architectures are similar to SOA patterns in their use of specialized, loosely coupled services. But they go even further in breaking down traditional architectures. The services within the microservices architecture use a common messaging framework, like RESTful APIs. They use RESTful APIs to communicate with each other without difficult data conversion transactions or additional integration layers. Using RESTful APIs allows, and even encourages, faster delivery of new features and updates. Each service is discrete. One service can be replaced, enhanced, or dropped without affecting any other service in the architecture. This lightweight architecture helps optimize distributed or cloud resources and supports dynamic scalability for individual services.

---

# 1. First: the starting point — Monolithic architecture

Before SOA or microservices, most software looked like this:

```
One giant application
```

Example system:

```
E-commerce app
```

Inside it:

```
User login
Product catalog
Payments
Inventory
Shipping
Analytics
```

Everything is inside **one codebase** and one deployable program.

```
[ Monolithic App ]
   ├ user module
   ├ payment module
   ├ inventory module
   ├ shipping module
```

### Problem

If you change one thing:

- the whole system must be redeployed
    
- bugs can break unrelated features
    
- scaling is difficult
    

Example:

If checkout traffic increases, you must scale **the entire system**, not just payments.

---

# 2. SOA (Service-Oriented Architecture)

SOA was the **first attempt to break the monolith**.

Instead of one giant program, you split functions into **services**.

Example:

```
User service
Payment service
Inventory service
Shipping service
```

Architecture:

```
User App
   │
   ▼
Enterprise Service Bus (ESB)
   │
   ├ Payment Service
   ├ Inventory Service
   ├ Shipping Service
```

The key component is the **ESB (Enterprise Service Bus)**.

Think of it like a **central communication hub**.

All services talk through it.

---

## Why SOA helped

It allowed companies to reuse services.

Example:

```
Payment service
```

Could be used by:

- website
    
- mobile app
    
- internal accounting system
    

So systems became **loosely coupled**.

Meaning:

Services depend on each other **less tightly**.

---

## The problem with SOA

The ESB became **too powerful**.

Everything had to pass through it.

Example:

```
Service A → ESB → Service B
```

Over time the ESB handled:

- routing
    
- data transformation
    
- security
    
- logging
    
- business logic
    

It became a **massive bottleneck**.

Also, when one service changed:

```
Service change → ESB changes → multiple services break
```

This is the “cascading change” problem mentioned in the paragraph.

---

# 3. Microservices architecture

Microservices is the **modern evolution**.

Instead of:

```
services connected through a central bus
```

You have **independent small services** talking directly.

Example architecture:

```
User Service
Product Service
Payment Service
Order Service
Notification Service
```

Communication happens via APIs.

Example:

```
Order Service
     │
     ▼
Payment Service API
```

Usually through:

```
REST APIs
```

---

# 4. The key difference

SOA:

```
services
   │
   ▼
ESB (central brain)
   │
   ▼
other services
```

Microservices:

```
service → API → service
```

No central hub controlling everything.

Each service is **independent**.

---

# 5. Why microservices became popular

Microservices make systems easier to scale and develop.

### Example: Netflix

The streaming platform  
Netflix  
runs thousands of microservices.

Example services:

```
Recommendation service
Playback service
User profile service
Search service
Billing service
```

Each service can scale independently.

If recommendation traffic spikes:

Only that service scales.

---

# 6. Why REST APIs matter here

Microservices communicate through APIs.

Example:

```
Order service → POST /payments
```

Because APIs are standardized:

Services written in different languages can communicate.

Example:

```
Payment service → Java
Order service → Go
Recommendation service → Python
```

They just talk through **HTTP + JSON**.

---

# 7. What the paragraph means by “lightweight architecture”

Microservices remove heavy integration layers.

SOA:

```
Service → ESB → Service
```

Microservices:

```
Service → API → Service
```

Simpler communication.

---

# 8. Why microservices scale well in the cloud

Cloud systems (like AWS) work well with distributed services.

Example:

```
Load balancer
   │
   ├ User service (3 servers)
   ├ Payment service (5 servers)
   ├ Search service (10 servers)
```

Each service scales independently.

This is called **dynamic scalability**.

---

# 9. A real-world analogy

Monolith:

```
One giant department store
```

Everything inside one building.

SOA:

```
Multiple stores connected through a central mall
```

Microservices:

```
Independent small shops in a city
```

Each shop runs independently but interacts with others.

---

# 10. Why this matters for API thinking

APIs became essential because **services need a way to talk to each other**.

Modern architecture looks like:

```
Service A
   │
   ▼
REST API
   │
   ▼
Service B
```

The internet today is basically:

```
Millions of microservices communicating through APIs
```

---

Since you're learning **API thinking**, there’s actually a deeper idea here that many technical founders eventually realize:

**Microservices + APIs changed how companies are built internally.**

Companies like:

- Amazon
    
- Uber
    
- Spotify
    

basically run as **internal API ecosystems**.

---

