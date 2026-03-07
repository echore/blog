---
share: true
---
2026-03-07  14:51
Tags:[[Technical Literacy|Technical Literacy]]

# One sentence to remember

API:

> “Let me check if something happened.”

Webhook:

> “I’ll tell you when something happens.”

---

# 1. First: normal API communication

A normal API works like **asking a question**.

Client → Server

Example:

```http
GET /orders/123
```

You are asking:

> “Do you have data for order 123?”

The server replies.

So the pattern is:

```
Client asks → Server responds
```

This is called **request–response**.

Example services using this pattern:

- Stripe API
    
- Reddit API
    
- Notion API
    

You ask for data when **you want it**.

---

# 2. The problem with APIs for events

Imagine you run a payment system.

You want to know:

> “When did a customer pay?”

If you only use APIs, you must keep asking.

Example:

```
GET /payments
GET /payments
GET /payments
GET /payments
```

This is called **polling**.

You're constantly asking the server:

> “Anything new yet?”

Most requests return **nothing**.

This wastes resources.

---

# 3. The webhook idea

A webhook flips the direction.

Instead of asking repeatedly, you say:

> “When something happens, notify me.”

Example:

```
Stripe → your server
```

When a payment happens:

Stripe sends:

```http
POST /webhook/payment
```

Payload:

```json
{
 "event": "payment_success",
 "amount": 2000,
 "customer": "cus_123"
}
```

Your server receives it instantly.

---

# 4. The key difference

### Normal API

You pull data.

```
Client → request → Server
```

Example:

```
GET /payments
```

---

### Webhook

The server pushes data.

```
Server → notification → Client
```

Example:

```
POST /webhook/payment
```

---

# 5. Why the article calls webhooks “reverse APIs”

Because the direction flips.

Normal API:

```
You → server
```

Webhook:

```
Server → you
```

That’s why people say:

**push vs pull**

|Pattern|Who initiates|
|---|---|
|API|client pulls data|
|Webhook|server pushes data|

---

# 6. Real-world example

Let’s use  
Stripe again.

When a payment succeeds, Stripe sends a webhook.

Example event:

```
payment_intent.succeeded
```

Stripe automatically sends:

```http
POST https://yourapp.com/webhook
```

With the payment data.

Your system can then:

- update the order
    
- send a receipt
    
- unlock content
    

All automatically.

---

# 7. Another example: GitHub

The platform  
GitHub  
uses webhooks for automation.

When someone pushes code:

```
push event
```

GitHub sends a webhook to a CI/CD system.

Example workflow:

```
GitHub → webhook → build server
```

Then:

- tests run
    
- deployment starts
    

This is how **continuous deployment** works.

---

# 8. Why webhooks are perfect for automation

Because they are **event-driven**.

Something happens → automation runs.

Example:

```
Payment received
      ↓
Webhook
      ↓
Send email
      ↓
Update database
```

Tools like **n8n** rely heavily on this pattern.

---

# 9. The important line in the text

> “An application must have an API to use a webhook.”

This means:

Webhooks don’t replace APIs.

They **work with them**.

Example flow:

```
Stripe webhook → your server
           ↓
Your server calls Stripe API
           ↓
GET /payment_details
```

The webhook tells you **something happened**.

The API lets you **fetch full data**.

---

# 10. A simple mental model

Think of APIs and webhooks like communication styles.

API:

```
You call someone to ask for information
```

Webhook:

```
Someone calls you when something happens
```

---

# 11. Why this matters for your automation work

If you build systems like:

```
Reddit → n8n → Notion
```

Right now you're probably using **API polling**.

Example:

```
Check Reddit every hour
```

But some systems use webhooks:

```
New event → trigger automation
```

This is **much more efficient**.

---

