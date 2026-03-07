---
share: true
---
2026-03-07  16:00
Tags:[[Technical Literacy|Technical Literacy]]

Follow by [[RESTful API - Basics|RESTful API - Basics]]


# 1 Resource Identifiers  and  Hypermedia

---

# 1. Resource Identifiers (URI)

The text says:

> REST uses resource identifiers to identify each resource involved in the interactions.

Plain meaning:

> Every piece of data in a REST system has a **unique address (URL)**.

That address is called a **URI / resource identifier**.

Think of it like **a street address for data**.

Example API:

```
https://api.github.com/users
```

This identifies the **users resource**.

Specific user:

```
https://api.github.com/users/yachen
```

Specific repository:

```
https://api.github.com/repos/openai/gpt
```

So the pattern is:

```
/resource
/resource/id
/resource/id/subresource
```

Example with Reddit:

```
https://www.reddit.com/r/financialindependence
```

Specific post:

```
https://www.reddit.com/comments/abc123
```

So the key idea:

> **Every resource must have a unique identifier (URL).**

This is one of the **core REST principles**.

---

# 2. Representation

REST does not send the **actual resource**, it sends a **representation** of it.

Example:

A Reddit post exists in the database like this:

```
post
id
title
author
upvotes
comments
created_time
```

But when the API sends it to you, it sends a **representation**:

```json
{
 "title": "Best FIRE strategy",
 "author": "user123",
 "upvotes": 5200
}
```

That JSON is a **representation of the resource**.

REST term:

```
resource → representation
```

---

# 3. Media Type

The paragraph says:

> The data format of a representation is known as a media type.

This simply means **the format of the response**.

Common media types:

|Media type|Meaning|
|---|---|
|application/json|JSON data|
|text/html|HTML page|
|application/xml|XML data|
|text/plain|plain text|

Example response header:

```
Content-Type: application/json
```

That tells the client:

> The server is sending JSON.

Which is why your automation tools know how to parse it.

---

# 4. Hypermedia (this is the confusing one)

This part is the most theoretical REST concept.

The text says:

> A RESTful API looks like hypertext.

Meaning:

> API responses contain **links to other resources**.

Example response:

```json
{
 "user": "yachen",
 "repos_url": "https://api.github.com/users/yachen/repos",
 "followers_url": "https://api.github.com/users/yachen/followers"
}
```

Notice:

```
repos_url
followers_url
```

Those are **links to other resources**.

So the API response itself tells you:

- where to go next
    
- what data you can access
    

This is called **HATEOAS**:

```
Hypermedia As The Engine Of Application State
```

Very famous REST concept.

---

# 5. Real-world example

Imagine a **book API**.

You request:

```
GET /books/42
```

Response:

```json
{
 "id": 42,
 "title": "The Pragmatic Programmer",
 "author": "Andy Hunt",
 "reviews": "/books/42/reviews",
 "publisher": "/publishers/12"
}
```

Those URLs allow you to navigate the API.

That’s **hypermedia**.

---

# 6. Why most APIs ignore this

Here’s a funny truth.

Most real APIs:

- Reddit
    
- Stripe
    
- Notion
    
- OpenAI
    
- Shopify
    

**do NOT fully implement hypermedia**.

They mostly just give JSON data.

Example Reddit response:

```json
{
 "title": "How I retired early",
 "ups": 4300,
 "num_comments": 210
}
```

No navigation links.

So modern APIs are often called:

```
REST-like APIs
```

rather than pure REST.

---

# 7. The practical takeaway

When building or using APIs, the **important parts are**:

1️⃣ Resources have URLs

```
/posts
/posts/123
```

2️⃣ Actions use HTTP methods

```
GET
POST
PATCH
DELETE
```

3️⃣ Responses return representations

```
JSON
```

4️⃣ Optional links connect resources

```
/posts/123/comments
```

---

# A mental model that helps

Think of a REST API like a **file system on the internet**.

```
/users
/users/123
/users/123/posts
/users/123/posts/456
```

Each path is a **resource identifier**.

The server just returns **representations of those files**.

---




# 2 Self-descriptive


This paragraph is describing a **very specific REST principle** called **“self-descriptive messages.”** The wording is academic, but the core idea is actually simple. Let’s decode it step-by-step.

---

# 1. What “self-descriptive” means

The text says:

> resource representations shall be self-descriptive.

Plain English:

> When the server sends data, the message should contain enough information for the client to understand **how to process it**.

The client should not need **extra hidden knowledge** about the server.

In practice, this is achieved with things like:

- **Content-Type**
    
- **media types**
    
- **standard formats**
    

Example response:

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

Body:

```json
{
  "name": "Yachen",
  "role": "student"
}
```

From the header alone, the client knows:

- this is **JSON**
    
- parse it as JSON
    

So the message **describes itself**.

---

# 2. What is a media type?

A **media type** tells the client **how to interpret the data format**.

Example media types:

|Media Type|Meaning|
|---|---|
|application/json|JSON data|
|text/html|HTML document|
|application/xml|XML|
|image/png|PNG image|

Example:

```http
Content-Type: text/html
```

The browser knows:

> render this as a webpage.

Example:

```http
Content-Type: image/png
```

The browser knows:

> display this as an image.

So the **media type explains how to process the data**.

---

# 3. Why the paragraph mentions HTML

HTML is actually a great example of **self-descriptive media types**.

Example HTML:

```html
<a href="https://example.com">Click</a>
```

The browser knows automatically:

- `<a>` = link
    
- `href` = destination
    
- clicking it triggers **GET request**
    

The browser **does not need special instructions from the server**.

Everything is defined by the **HTML media type specification**.

That’s what the paragraph means here:

> HTML defines a rendering process and behavior.

---

# 4. Custom media types in REST APIs

The text says:

> we create lots of custom media types.

In theoretical REST systems, APIs sometimes define **custom media types**.

Example:

```http
Content-Type: application/vnd.github+json
```

This means:

> JSON formatted specifically according to GitHub's API structure.

Stripe does similar things.

Example:

```http
Content-Type: application/vnd.stripe+json
```

So the client knows:

- this is JSON
    
- but with **Stripe's structure**
    

---

# 5. Important clarification in the paragraph

The text says:

> Media types have no relation to HTTP methods.

This is important.

Media types describe **data format**.

HTTP methods describe **actions**.

So they are **two separate concepts**.

|Concept|Purpose|
|---|---|
|HTTP method|action|
|media type|data format|

Example request:

```http
POST /users
Content-Type: application/json
```

Here:

- `POST` = action (create user)
    
- `application/json` = format of the data
    

They are independent.

---

# 6. Example of a full REST interaction

Request:

```http
POST /users
Content-Type: application/json
```

Body:

```json
{
  "name": "Yachen"
}
```

Response:

```http
HTTP/1.1 201 Created
Content-Type: application/json
```

Body:

```json
{
  "id": 42,
  "name": "Yachen"
}
```

Everything the client needs to understand is inside the message.

That’s **self-descriptive communication**.

---

# 7. Why this matters in practice

This principle allows **different systems to interact without prior agreement**.

Example:

- browser
    
- mobile app
    
- automation tool
    
- server
    

All communicate using:

- HTTP methods
    
- media types
    
- standardized formats
    

So any system that understands:

```http
application/json
```

can talk to the API.

---

# 8. Reality check (important)

In theory REST is very strict.

In practice most APIs are simpler.

Typical modern API:

```http
GET /posts
```

Response:

```http
Content-Type: application/json
```

Body:

```json
{
 "title": "Best FIRE strategy"
}
```

That's already **good enough for most systems**.

So many APIs don't bother with complicated custom media types.

---

# 9. The mental model

You can think of REST messages like **shipping packages**.

Every package includes:

- label (headers)
    
- instructions (media type)
    
- content (body)
    

Example:

```
Label: application/json
Content: {"name": "Yachen"}
```

The receiver immediately knows **how to unpack it**.

---

# 10. The deeper REST philosophy

REST wants systems where:

- messages explain themselves
    
- resources have addresses
    
- clients discover behavior through media types and links
    

This creates **loosely coupled systems**.

Meaning:

> the client and server don't need to know each other's internal design.

---






