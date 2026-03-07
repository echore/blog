---
share: true
---
2026-03-07  15:46
Tags:[[Technical Literacy|Technical Literacy]]

## Great video:
https://youtu.be/-MTSQjw5DrM?si=ePbvf9bPzXIusJyV 
It has an example by javascript

https://youtu.be/lsMQRaeKNDk?si=Mij4mYfrseV5mL0n from IBM I like this more, really good, definitely worth rewatching.
It's all about **communication**!!!!!!

![[Pasted image 20260307162647.png|Pasted image 20260307162647.png]]



Great question. Let’s unpack **RESTful APIs** in a way that actually helps you understand what’s happening in your **n8n + Reddit + Notion workflows**, not just theory.

Think of a REST API like a **restaurant system**.

- The **menu** = API endpoints
    
- The **waiter** = HTTP request
    
- The **kitchen** = server
    
- The **dish** = JSON response
    

You ask for something → server brings it back.

---

# 1. The core idea of REST: resources

REST APIs revolve around **resources**.

A **resource = a piece of data on the server**.

Examples:

|Resource|Example|
|---|---|
|user|user profile|
|post|Reddit post|
|comment|Reddit comment|
|task|todo item|
|page|Notion page|

Each resource has a **URL**.

Example:

```
https://api.reddit.com/r/financialindependence
```

That URL represents the **subreddit resource**.

Another example:

```
https://api.notion.com/v1/pages
```

That represents **Notion pages**.

So REST basically says:

> Everything on the server should be treated as a resource with a URL.

---

# 2. [[API - HTTP methods|API - HTTP methods]] (the verbs of REST)

REST APIs use **HTTP methods** to interact with resources.

These are the **actions** you can take.

|Method|Meaning|Example|
|---|---|---|
|GET|read|get Reddit posts|
|POST|create|create Notion page|
|PUT|replace|update object|
|PATCH|partial update|modify fields|
|DELETE|remove|delete item|

Example:

### Get data

```
GET https://api.reddit.com/r/financialindependence/top.json
```

Server returns:

```json
{
  "title": "How I retired at 35",
  "upvotes": 5400
}
```

---

### Create data

```
POST https://api.notion.com/v1/pages
```

Body:

```json
{
  "title": "New research note"
}
```

Server creates a new page.

---

This pattern is **very consistent across almost every API**.

---

# 3. Endpoints (the doors into the system)

An **endpoint = a specific API URL**.

Example:

```
/users
/users/123
/posts
/posts/456
```

Think of them like **database tables exposed through URLs**.

Example:

|Endpoint|Meaning|
|---|---|
|/users|all users|
|/users/123|specific user|
|/posts|all posts|
|/posts/456|specific post|

Example request:

```
GET https://api.github.com/users/yachen
```

Server returns a user object.

---

# 4. JSON (how data travels)

Most REST APIs return **JSON**.

Example response:

```json
{
  "title": "Best FIRE strategy",
  "upvotes": 2300,
  "comments": 187
}
```

Why JSON?

Because every programming language understands it.

Python:

```
dict
```

JavaScript:

```
object
```

n8n:

```
$json
```

So when you do:

```
{{$json.data.title}}
```

You are literally accessing a **JSON field from the API response**.

---

# 5. REST is stateless

This is a **key concept**.

REST APIs are **stateless**.

Meaning:

> Every request is independent.

The server does **not remember previous requests**.

Example:

```
GET /posts
GET /posts
GET /posts
```

Each request is processed separately.

This makes REST APIs **very scalable**.

That’s why massive systems like:

- Reddit
    
- Stripe
    
- Shopify
    
- Twitter
    

all use REST.

---

# 6. Status codes (server responses)

Servers respond with **HTTP status codes**.

|Code|Meaning|
|---|---|
|200|success|
|201|created|
|400|bad request|
|401|unauthorized|
|404|not found|
|500|server error|

Example:

```
200 OK
```

means the request worked.

In n8n you'll often see:

```
statusCode: 200
```

---

# 7. Query parameters

These modify requests.

Example:

```
https://www.reddit.com/r/financialindependence/top.json?t=week&limit=10
```

Parameters:

|Parameter|Meaning|
|---|---|
|t=week|time range|
|limit=10|number of posts|

These are called **query parameters**.

Syntax:

```
?key=value&key=value
```

---

# 8. Headers

Headers send **extra information**.

Example:

```
Authorization: Bearer API_KEY
Content-Type: application/json
```

Examples:

|Header|Purpose|
|---|---|
|Authorization|API key|
|Content-Type|data format|
|User-Agent|client identifier|

Reddit often requires:

```
User-Agent: my-app
```

---

# 9. The REST request structure

A REST request has **four parts**.

```
METHOD
URL
HEADERS
BODY
```

Example:

```
POST /v1/pages
Host: api.notion.com
Authorization: Bearer xxx
Content-Type: application/json
```

Body:

```json
{
 "title": "Research notes"
}
```

---

# 10. Why this matters for you

Because **understanding REST unlocks almost every modern tool**.

Your stack already uses it:

Reddit API

```
GET /top.json
```

Notion API

```
POST /pages
```

OpenAI API

```
POST /chat/completions
```

n8n is basically:

```
REST API → process → REST API
```

Which means you are already learning **backend system thinking**.

---

# One deeper insight most beginners miss

REST APIs are basically **databases exposed over the internet**.

Example:

```
GET /users
```

is basically:

```
SELECT * FROM users
```

```
POST /users
```

is:

```
INSERT INTO users
```

Once you see that, the whole API ecosystem becomes much easier.

---

