---
share: true
---
2026-03-07  15:55
Tags:[[Technical Literacy|Technical Literacy]]



---

# 1. What an HTTP method actually is

An **HTTP method** tells the server **what action you want to perform on a resource**.

Think of it like the **verb in a sentence**.

Example sentence:

> I **read** a book.

- book = resource
    
- read = action
    

In HTTP:

```
GET /posts
```

- `/posts` = resource
    
- `GET` = action
    

So:

> HTTP method = the **operation you want to perform on data**.

---

# 2. The 4 most important HTTP methods

In practice, **90% of APIs use just four methods**.

|Method|Meaning|What it does|
|---|---|---|
|GET|retrieve|read data|
|POST|create|add new data|
|PUT / PATCH|update|modify data|
|DELETE|delete|remove data|

These correspond almost perfectly to **database operations**.

|HTTP|Database|
|---|---|
|GET|SELECT|
|POST|INSERT|
|PUT/PATCH|UPDATE|
|DELETE|DELETE|

So APIs are basically **remote databases accessed via HTTP**.

---

# 3. GET — retrieve data

**GET is the most common method.**

It asks the server to **send back data**.

Example:

```
GET https://api.reddit.com/r/financialindependence/top.json
```

The server responds with JSON:

```json
{
 "title": "Best FIRE strategy",
 "upvotes": 1340
}
```

Important characteristics:

- **does not change data**
    
- safe to repeat
    
- used for reading
    

Example APIs using GET:

- fetch tweets
    
- fetch Reddit posts
    
- fetch user profile
    
- fetch product list
    

---

# 4. POST — create something

POST means:

> create a new resource.

Example:

```
POST https://api.notion.com/v1/pages
```

Body:

```json
{
 "title": "Research notes"
}
```

The server creates a **new page**.

POST is used when:

- creating a user
    
- adding a comment
    
- creating a payment
    
- inserting data into a database
    

---

# 5. PUT vs PATCH — update data

Both modify existing resources.

### PUT

PUT replaces the entire object.

Example:

```
PUT /users/123
```

Body:

```json
{
 "name": "Yachen",
 "age": 24
}
```

This replaces the whole record.

---

### PATCH

PATCH updates **only part of the object**.

Example:

```
PATCH /users/123
```

Body:

```json
{
 "age": 25
}
```

Only the age changes.

Most modern APIs use **PATCH** instead of PUT.

---

# 6. DELETE — remove something

DELETE removes a resource.

Example:

```
DELETE /posts/456
```

Server deletes post **456**.

Common use cases:

- delete comment
    
- delete account
    
- delete item in cart
    

---

# 7. A real REST example

Imagine a **todo app API**.

Create task:

```
POST /tasks
```

Read tasks:

```
GET /tasks
```

Update task:

```
PATCH /tasks/42
```

Delete task:

```
DELETE /tasks/42
```

This structure is used everywhere.

---

# 8. How this appears inside n8n

When you configure an **HTTP Request node**, you choose the method.

Example for Reddit:

Method:

```
GET
```

URL:

```
https://www.reddit.com/r/financialindependence/top.json
```

Because you're **retrieving data**.

---

If you were writing to Notion:

Method:

```
POST
```

Because you're **creating a new page**.

---

# 9. One subtle concept (important)

HTTP methods also describe **side effects**.

|Method|Safe|Changes server?|
|---|---|---|
|GET|yes|no|
|POST|no|yes|
|PUT|no|yes|
|PATCH|no|yes|
|DELETE|no|yes|

GET should **never change data**.

That’s why browsers can safely cache GET requests.

---

# 10. Mental model that helps a lot

Think of an API as **a remote database table**.

Example table:

```
posts
```

|id|title|
|---|---|
|1|Hello|
|2|FIRE strategy|

Operations:

Read:

```
GET /posts
```

Insert:

```
POST /posts
```

Update:

```
PATCH /posts/2
```

Delete:

```
DELETE /posts/2
```

So **HTTP methods = database operations over the internet**.

---

Since you're building **automation workflows**, the next concept that will make everything click is actually:

**the full anatomy of an API request**:

```
Method
URL
Headers
Body
Query parameters
```

Once you understand that structure, you'll be able to **look at any API documentation and instantly know how to use it**.