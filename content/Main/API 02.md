---
share: true
---
2026-03-07  14:23
Tags:[[Technical Literacy|Technical Literacy]]

### API basics

Good explanation:

[https://www.redhat.com/en/topics/api/what-are-application-programming-interfaces](https://www.redhat.com/en/topics/api/what-are-application-programming-interfaces)


APIs are a simplified way to connect your own infrastructure through cloud-native app development, but they also allow you to share your data with customers and other external users. Public APIs represent unique business value because they can simplify and expand how you connect with your partners, as well as potentially monetize your data (the Google Maps API is a popular example).

![[Pasted image 20260307141656.png|Pasted image 20260307141656.png]]


For example, imagine a book-distributing company. The book distributor could give its customers a [cloud app](https://www.redhat.com/en/topics/cloud-native-apps/what-are-cloud-applications) that lets bookstore clerks check book availability with the distributor. This app could be expensive to develop, limited by platform, and require long development times and ongoing maintenance.

Alternatively, the book distributor could provide an API to check stock availability. There are several benefits to this approach:

- Letting customers access data via an API helps them aggregate information about their inventory in a single place.
- The book distributor can make changes to its internal systems without impacting customers, so long as the behavior of the API doesn’t change.
- With a publicly available API, developers working for the book distributor, book sellers or third parties could develop an app to help customers find the books they’re looking for. This could result in higher sales or other business opportunities.

In short, APIs let you open up access to your resources while maintaining [security](https://www.redhat.com/en/topics/security) and control. How you open access and to whom is up to you. [API security](https://www.redhat.com/en/topics/security/api-security) is all about good API management, which includes the use of an [API gateway](https://www.redhat.com/en/topics/api/what-does-an-api-gateway-do). Connecting to APIs, and creating applications that consume the data or functionality exposed by APIs, can be done with a distributed integration platform that connects everything—including legacy systems, and the [Internet of Things (IoT)](https://www.redhat.com/en/topics/internet-of-things/what-is-iot).

---
## Explanation:

# 1. The old way (building an app for customers)

Imagine a **book distributor** (a company that sells books to bookstores).

Bookstores constantly need to ask:

> “Do you have this book in stock?”

The distributor has two options.

### Option A — Build a custom app

The distributor builds a **software app** for bookstores.

Example:

- A web portal
    
- A mobile app
    
- A desktop system
    

Bookstore clerks log in and search for books.

But this has problems:

**Problem 1 — expensive**

You must build:

- iOS app
    
- Android app
    
- web app
    

Lots of engineering work.

---

**Problem 2 — slow development**

If bookstores want new features:

> “Can we export inventory to Excel?”

Now the distributor must rebuild the software.

---

**Problem 3 — limited flexibility**

Every bookstore must use **your app**.

But bookstores already have:

- POS systems
    
- inventory systems
    
- ERP software
    

Your app doesn't integrate with them.

---

# 2. The API approach (the modern solution)

Instead of building an app, the distributor exposes an **API**.

Example API:

```
GET /books?isbn=9780143126560
```

Response:

```json
{
 "title": "The Intelligent Investor",
 "stock": 142
}
```

Now bookstores can connect however they want.

Examples:

- their inventory system calls the API
    
- their POS system checks stock automatically
    
- their website checks availability
    

So instead of:

```
Human → app → distributor
```

You now have:

```
Software → API → distributor
```

This is **machine-to-machine communication**.

---

# 3. Why APIs are powerful (the paragraph’s main point)

The paragraph lists **three big advantages**.

---

## Benefit 1

### Customers can combine data in one system

A bookstore might work with **5 distributors**.

Without APIs:

They must check 5 different websites.

With APIs:

Their inventory software automatically checks all distributors.

Example:

```
Bookstore system
     ↓
Distributor A API
Distributor B API
Distributor C API
```

Everything is in **one dashboard**.

---

## Benefit 2

### The distributor can change internal systems safely

This is a big concept.

Customers interact with the **API**, not your internal system.

Example:

Before:

```
API → Old Database
```

Later you upgrade:

```
API → New Cloud System
```

As long as the API responses stay the same:

```
stock: 142
```

Customers don't notice.

The API acts like a **stable interface**.

---

## Benefit 3

### Third-party developers can build new tools

This is the **platform effect**.

If your API is public, other people can build things.

Example apps:

- book price comparison apps
    
- library inventory systems
    
- bookstore management tools
    
- marketplace platforms
    

Example:

```
Goodreads
     ↓
Book distributor API
     ↓
Shows real-time availability
```

Now your books sell more.

This is how **platform ecosystems** form.

Examples in real life:

|Company|API ecosystem|
|---|---|
|Stripe|payment apps|
|Google Maps|delivery apps|
|Twitter|analytics tools|
|OpenAI|AI apps|

APIs allow **external innovation**.

---

# 4. "Open access while maintaining control"

This line means:

You let people use your system **without giving them full access**.

Think of it like:

```
Restaurant kitchen
```

Customers don't enter the kitchen.

They interact through the **waiter (API)**.

The API decides:

- what requests are allowed
    
- what data is visible
    
- how often requests are allowed
    

This keeps systems secure.

---

# 5. What API management means

Large companies don't just expose APIs randomly.

They manage them carefully.

This includes:

- authentication
    
- rate limits
    
- monitoring
    
- logging
    
- versioning
    

Example:

```
API key required
```

```
Authorization: Bearer xxxxx
```

Only authorized clients can access the API.

---

# 6. What an API gateway is

An **API gateway** is like a **front desk** for all APIs.

Instead of clients talking to many services:

```
Client → Service A
Client → Service B
Client → Service C
```

Everything goes through:

```
Client
   ↓
API Gateway
   ↓
Service A
Service B
Service C
```

The gateway handles:

- authentication
    
- request routing
    
- security
    
- monitoring
    
- rate limits
    

Examples of API gateways:

- AWS API Gateway
    
- Kong
    
- Apigee
    
- Cloudflare API Gateway
    

---

# 7. "Distributed integration platform"

This phrase sounds complicated but it's simple.

It means **software that connects different systems together**.

Example tools:

|Tool|What it does|
|---|---|
|Zapier|connects SaaS apps|
|n8n|workflow automation|
|MuleSoft|enterprise integrations|
|Workato|enterprise automation|

Your **n8n setup is exactly this**.

Example:

```
Reddit API
     ↓
n8n workflow
     ↓
Filter posts
     ↓
Notion API
```

You built a **distributed integration system**.

---

# 8. The final line: "connecting legacy systems and IoT"

This means APIs can connect:

### Legacy systems

Old software like:

- hospital databases
    
- bank mainframes
    
- government systems
    

APIs allow modern apps to talk to them.

---

### IoT devices

Internet-connected devices:

- smart thermostats
    
- factory sensors
    
- delivery robots
    

Example:

```
Temperature sensor → API → cloud dashboard
```

---

# 9. The big business idea behind APIs

APIs transform companies from:

**products → platforms**

Instead of just selling something:

You create an **ecosystem others build on**.

Example:

```
Amazon → AWS APIs
Stripe → payment APIs
OpenAI → AI APIs
```

This is why APIs are one of the **most powerful business models in tech**.

---


## Innovating with APIs

Suppose one of the company's partners develops an app that helps people find books on bookstore shelves. This improved experience brings more shoppers to the bookstore—the distributor's customer—and extends an existing revenue channel.

Maybe a third party uses a public API to develop an app that lets people buy books directly from the distributor, instead of from a store. This opens a new revenue channel for the book distributor.

Sharing APIs―with select partners or the whole world―can have positive effects. Each partnership extends your brand recognition beyond your company’s marketing efforts. Opening technology to everyone, as with a public API, encourages developers to build an ecosystem of apps around your API. More people using your technology means more people are likely to do business with you.

Making technology public can lead to novel and unexpected outcomes. These outcomes sometimes disrupt entire industries. For our book distributing company, new firms―a book borrowing service, for example―could fundamentally change the way they do business. Partner and public APIs help you use the creative efforts of a community larger than your team of internal developers. New ideas can come from anywhere, and companies need to be aware of changes in their market and ready to act on them. APIs can help.

