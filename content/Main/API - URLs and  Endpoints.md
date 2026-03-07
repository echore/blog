---
share: true
---
2026-03-07  16:34
Tags:[[Technical Literacy|Technical Literacy]]


---

# 1. First: What is a URL?

A **URL (Uniform Resource Locator)** is simply an **address on the internet**.

Example:

```id="s49kbr"
https://www.reddit.com
```

Just like a physical address:

```
742 Evergreen Terrace
Springfield
USA
```

A URL tells the computer:

- **which server**
    
- **where on that server**
    
- **what resource**
    

---

# 2. What is an API endpoint?

An **endpoint** is a **specific URL where an API provides data or services**.

Example:

```id="f2f39b"
https://api.github.com/users
```

This endpoint returns **user data**.

Another endpoint:

```id="d6p6k1"
https://api.github.com/repos
```

This returns **repository data**.

So an endpoint is basically:

> **a door into the server's data**

Each door gives you **different information**.

---

# 3. Example using Reddit (very concrete)

Example endpoint:

```id="yuf0d7"
https://www.reddit.com/r/financialindependence/top.json
```

This endpoint returns:

- top posts
    
- from subreddit `financialindependence`
    
- in JSON format
    

So the API endpoint describes:

|Part|Meaning|
|---|---|
|reddit.com|the server|
|/r/financialindependence|the resource|
|/top|the operation|
|.json|return format|

---

# 4. Endpoints are usually structured like folders

Most APIs follow a **hierarchical structure**.

Example:

```id="2laz9c"
/users
/users/42
/users/42/posts
/users/42/followers
```

Think of it like a **file system**.

Example folder structure:

```
users/
   42/
      posts/
      followers/
```

Each path is a **different endpoint**.

---

# 5. Real-world API example

Imagine a **shopping website API**.

Possible endpoints:

```id="jix4a4"
/products
/products/15
/products/15/reviews
/orders
/orders/108
```

Meaning:

|Endpoint|Meaning|
|---|---|
|/products|list all products|
|/products/15|product with ID 15|
|/products/15/reviews|reviews for that product|
|/orders|all orders|
|/orders/108|specific order|

So endpoints represent **resources and relationships**.

---

# 6. The full URL structure

A typical API URL looks like this:

```id="qg4qyi"
https://api.example.com/users/42
```

Breakdown:

|Part|Meaning|
|---|---|
|https|protocol|
|api.example.com|server|
|/users/42|resource|

So this means:

> Ask the server **api.example.com** for user **42**.

---

# 7. Why APIs use "api."

Many APIs use a special subdomain:

```id="q8m8ds"
api.example.com
```

Instead of:

```id="yrup7u"
www.example.com
```

Reason:

- `www` → website for humans
    
- `api` → data for programs
    

Example:

```id="rtydrr"
https://api.stripe.com
https://api.github.com
https://api.notion.com
```

---

# 8. Endpoint + Method = API request

An endpoint alone is not enough.

You combine it with an **HTTP method**.

Example:

```id="huhgci"
GET https://api.example.com/users
```

Meaning:

> retrieve users.

Another example:

```id="p0sswp"
POST https://api.example.com/users
```

Meaning:

> create a new user.

So an API call always has:

```id="0rw8p4"
HTTP Method + Endpoint
```

---

# 9. How this appears in n8n

In your **HTTP Request node**, you fill:

Method:

```id="g8mztm"
GET
```

URL:

```id="rsrdho"
https://www.reddit.com/r/financialindependence/top.json
```

That URL is the **endpoint**.

n8n sends a request there and receives **JSON data**.

---

# 10. Quick intuition test

If you see this endpoint:

```id="yuh27i"
https://api.example.com/users/123/orders
```

You can probably guess:

It returns:

> **orders belonging to user 123**

Even without documentation.

That’s why REST APIs are designed this way — the endpoints are **human-readable**.

---

✅ **Key takeaway**

Endpoint = **the address where an API exposes a resource**

Example pattern:

```id="gzaq7c"
/resource
/resource/id
/resource/id/subresource
```

---

