---
share: true
---

2026-03-07  14:49
Tags: [[Technical Literacy|Technical Literacy]]
## SOAP vs. REST

# 1. First: SOAP vs REST (the simple intuition)

Think of them as **two ways to design APIs**.
![[Pasted image 20260307143216.png|Pasted image 20260307143216.png]]

Most modern APIs (Stripe, Reddit, OpenAI, Notion) are **REST APIs**.

---

# 2. SOAP (the older approach)

SOAP stands for:

**Simple Object Access Protocol**

SOAP APIs send messages in **XML format**.

Example SOAP request:

```xml
<Envelope>
  <Body>
    <GetBook>
      <ISBN>9780143126560</ISBN>
    </GetBook>
  </Body>
</Envelope>
```

Problems with SOAP:

- very verbose
    
- complicated standards
    
- heavy documentation
    
- hard for developers
    

SOAP was popular in **enterprise systems**, banks, and government.

But developers hated it.

---

# 3. REST (the modern approach)

REST stands for:

**Representational State Transfer**

It was proposed by  
Roy Fielding  
in his famous PhD dissertation in 2000.

REST is **not a strict protocol**.

Instead, it’s a design philosophy for APIs.

Example REST **request**:

```http
GET /books/9780143126560
```

Response:

```json
{
 "title": "The Intelligent Investor",
 "stock": 142
}
```

Much simpler.

---

# 4. Why REST won the internet

REST became dominant because it matches **how the web works**.

The web already uses:

- URLs
    
- HTTP
    
- resources
    

REST simply builds APIs using those concepts.

Example:

```
GET /users
GET /users/123
POST /users
DELETE /users/123
```

You can literally understand the API by reading the URL.

---

# 5. The key sentence you asked about

The paragraph says REST APIs follow **6 constraints**.

These come from Roy Fielding’s dissertation.

But don't worry — they’re mostly conceptual.

---

# [[RESTful API - Basics|RESTful API - Basics]]
# 6. The 6 REST constraints (in human language)

### 1️⃣ Client–Server separation

The client and server are independent.

Example:

```
App → API server
```

The client doesn't care how the server works internally.

This allows:

- mobile apps
    
- web apps
    
- other services
    

to use the same API.

---

### 2️⃣ Stateless communication

Each request must contain **all necessary information**.

The server should not remember previous requests.

Example:

Bad design:

```
request 1: login
request 2: get data
```

Good REST design:

```
GET /data
Authorization: Bearer token
```

Each request contains authentication.

Stateless systems scale better.

---

### 3️⃣ Cacheable responses

Responses should be cacheable when possible.

Example:

```
GET /products
```

The response might be cached for 5 minutes.

Benefits:

- faster responses
    
- lower server load
    

---

### 4️⃣ Uniform interface

This is the **core REST principle**.

Resources should have consistent URLs and methods.

Example:

```
GET /books
GET /books/123
POST /books
DELETE /books/123
```

Instead of weird endpoints like:

```
/fetchBookList
/getBookInfo
/removeBook
```

Uniform design makes APIs predictable.

---

### 5️⃣ Layered system

Clients don’t need to know if they're talking to:

- the actual server
    
- a proxy
    
- a cache
    
- a gateway
    

Example architecture:

```
Client
 ↓
CDN
 ↓
API Gateway
 ↓
Microservices
 ↓
Database
```

Clients just call the API.

---

### 6️⃣ Code on demand (optional)

Servers can send executable code to clients.

Example:

JavaScript sent to browsers.

But most APIs don’t use this.

This constraint is optional.

---

# 7. Why REST became dominant

REST matched how developers already think.

Instead of:

```
Execute operation: getBookData
```

REST says:

```
Access resource: /books/123
```

It treats everything as a **resource**.

Example resources:

```
/users
/orders
/products
/payments
```

---

# 8. What modern APIs actually look like

In reality, most APIs are **REST-ish**, not perfectly REST.

Example:

- Stripe API
    
- Notion API
    
- Reddit API
    
- OpenAI API
    

They follow REST ideas but not all 6 constraints strictly.

---

# 9. For your automation work

When you call this endpoint:

```
https://www.reddit.com/r/startups/top.json
```

You are using a **REST API**.

The structure:

```
GET /r/startups/top
```

Resource:

```
subreddit posts
```

Response:

```
JSON data
```

---

# 10. A simple mental model

SOAP thinking:

```
call remote procedure
```

REST thinking:

```
access resources via URLs
```

---

# 11. The big idea

REST turned APIs into something like **websites for machines**.

Instead of humans browsing pages:

```
Browser → website
```

Machines browse APIs:

```
Software → API
```

That idea powers almost the entire modern internet.

---




## 二 Stateless communication

---

# 1. What “state” means

**State = memory of previous interactions**

Example conversation with a waiter:

You say:

> I ordered pasta earlier.

The waiter remembers your order.

That system has **state** because it remembers history.

---

# 2. A stateful server (old style)

Imagine a login system like this:

Step 1:

```id="m1"
POST /login
username=alice
password=123
```

Server checks credentials and stores:

```id="m2"
User 847 logged in
```

Now the server remembers you.

Step 2:

```id="m3"
GET /data
```

Server checks its memory:

> Oh yes, user 847 is logged in.

Then it returns the data.

---

### The problem

The server must **store memory for every user**.

Example:

```id="m4"
User session table
------------------
User 847
User 921
User 301
User 122
```

If millions of users connect:

The server must track millions of sessions.

This becomes messy and hard to scale.

---

# 3. Stateless design (REST idea)

Instead of the server remembering users…

**Each request proves who you are.**

Step 1: login

```id="m5"
POST /login
```

Server returns a **token**.

Example:

```id="m6"
token = abc123xyz
```

---

Step 2: request data

Instead of the server remembering you…

You include the token:

```http
GET /data
Authorization: Bearer abc123xyz
```

Now the server checks the token.

It doesn't need to remember anything.

---

# 4. The key difference

Stateful:

```id="m8"
Server remembers you
```

Stateless:

```id="m9"
You prove who you are every request
```

---

# 5. Why stateless systems scale better

Imagine you run a huge service like  
Netflix.

Millions of users are sending requests.

If servers store sessions:

```id="m10"
User session memory
```

Requests must go to the **same server**.

Otherwise the session is lost.

That creates a bottleneck.

---

With stateless APIs:

Any server can handle the request.

Example architecture:

```id="m11"
Client
 ↓
Load balancer
 ↓
Server A
Server B
Server C
Server D
```

Every request contains:

```id="m12"
Authorization: Bearer token
```

So any server can verify it.

This makes scaling easy.

---

# 6. Why APIs love statelessness

Stateless systems allow:

- horizontal scaling
    
- load balancing
    
- caching
    
- microservices
    

Basically everything modern infrastructure needs.

---

# 7. Real example: your Reddit API call

When you call:

```id="m13"
https://www.reddit.com/r/startups/top.json
```

Reddit doesn't remember you.

Each request is independent.

It simply returns data.

Stateless.

---

# 8. Another real example: Stripe API

When apps call the  
Stripe API:

```http
POST /charges
Authorization: Bearer sk_live_xxx
```

Every request includes the API key.

Stripe doesn't need to remember previous calls.

Stateless.

---

# 9. The one-sentence intuition

Stateful system:

> “I remember who you are.”

Stateless system:

> “Prove who you are every request.”

---

# 10. Why this matters for builders

When you design systems with APIs, statelessness means:

Your system becomes:

- easier to scale
    
- easier to debug
    
- easier to distribute
    

That’s why REST emphasizes it.

---

If you want, I can also explain something **super useful for API literacy** (and it will immediately help with n8n and automation):

**Why APIs often return weird things like**

```
page=1
limit=50
cursor=abc123
```

That concept is called **pagination**, and it's one of the most important real-world API patterns.


## 四 Uniform interface

# 1. First: what is a “resource”?

In REST, everything is treated as a **resource**.

A resource is just **a thing in the system**.

Examples:

|Resource|Example URL|
|---|---|
|books|`/books`|
|users|`/users`|
|orders|`/orders`|
|payments|`/payments`|

Think of the API like a **collection of objects** you can interact with.

---

# 2. The REST idea: use HTTP methods consistently

Instead of inventing new verbs, REST uses the **same small set of actions everywhere**.

|HTTP method|Meaning|
|---|---|
|GET|read something|
|POST|create something|
|PATCH / PUT|update something|
|DELETE|remove something|

These actions stay **consistent across every resource**.

---

# 3. Example: a bookstore API

Resource:

```
books
```

Operations:

Get all books

```
GET /books
```

Get one book

```
GET /books/123
```

Add a new book

```
POST /books
```

Delete a book

```
DELETE /books/123
```

Notice something important:

The **URL stays about the resource**, not the action.

---

# 4. What bad APIs looked like before REST

Older APIs often looked like this:

```
/fetchBookList
/getBookInfo
/removeBook
/addBook
/updateBookPrice
```

Every action had its own endpoint.

Problems:

1️⃣ Hard to remember  
2️⃣ Inconsistent naming  
3️⃣ Difficult to design large APIs

Imagine hundreds of endpoints like this.

---

# 5. REST simplifies everything

Instead of inventing verbs:

The **HTTP method becomes the verb**.

Example:

|Action|REST design|
|---|---|
|get books|`GET /books`|
|get one book|`GET /books/123`|
|create book|`POST /books`|
|delete book|`DELETE /books/123`|

This makes the API **predictable**.

Even if you've never seen the API before, you can guess how it works.

---

# 6. Why this matters for developers

Once you understand the pattern, you can navigate any API quickly.

Example:

Suppose you see this:

```
/users
```

You can guess:

```
GET /users
```

→ list users

```
GET /users/42
```

→ get user 42

```
POST /users
```

→ create user

---

# 7. A real-world example: Stripe API

The  
Stripe API follows this style.

Example endpoints:

```
GET /v1/customers
POST /v1/customers
GET /v1/customers/{id}
DELETE /v1/customers/{id}
```

Once you learn the pattern, the entire API becomes easy to understand.

---

# 8. Why this is called a “uniform interface”

Uniform = consistent.

The same rules apply everywhere.

Instead of learning hundreds of different operations, developers only learn:

```
GET
POST
PATCH
DELETE
```

Then apply them to any resource.

---

# 9. A good mental model

Think of an API like a **database over the internet**.

Tables:

```
books
users
orders
```

Rows:

```
/books/123
/users/42
/orders/9001
```

Operations:

```
GET
POST
PATCH
DELETE
```

Uniform and predictable.

---

# 10. Why this principle was revolutionary

Before REST, APIs were chaotic.

After  
Roy Fielding  
introduced REST, APIs became **structured systems**.

That structure is why today:

- developers can learn new APIs quickly
    
- tools like Postman work across APIs
    
- automation tools (like your **n8n workflows**) work easily
    



