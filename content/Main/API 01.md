---
share: true
---
2026-03-07  14:15
Tags:[[Technical Literacy|Technical Literacy]]

Love this question. If you understand **API thinking**, your technical literacy jumps a lot — especially for the kind of automation and startup work you're already doing (n8n, scraping Reddit, connecting Notion, etc.).

Let’s build the concept **slowly and intuitively**, not like a CS textbook.

---

# 1. What an API actually is (in plain English)

**API = Application Programming Interface**

But honestly that definition is useless.

A better mental model:

**An API is a waiter in a restaurant.**

- You (the client) tell the waiter what you want.
    
- The waiter goes to the kitchen (the system).
    
- The waiter brings back your food (the data).
    

You **don’t go into the kitchen yourself**.

That’s exactly what APIs do.

Example:

You ask Reddit:

```
https://www.reddit.com/r/financialindependence/top.json?t=week&limit=10
```

You’re basically saying:

> Hey Reddit, give me the top 10 posts this week.

Reddit’s server sends back **data**.

Usually in **JSON format**.

---

# 2. The 3 core pieces of every API request

When you call an API, three things exist.

### 1️⃣ Endpoint

The **URL** you call.

Example:

```
https://api.openai.com/v1/chat/completions
```

Think of it as the **address of the kitchen**.

---

### 2️⃣ Request

What you send.

Usually:

- parameters
    
- headers
    
- body
    

Example:

```
limit=10
t=week
```

You are saying:

> give me the **top posts for the week**.

---

### 3️⃣ Response

The **data you get back**.

Usually JSON.

Example simplified:

```json
{
  "data": {
    "children": [
      {
        "title": "How I reached FIRE",
        "ups": 1200,
        "num_comments": 250
      }
    ]
  }
}
```

That’s the **raw data** your automation processes.

---

# 3. The key shift: API Thinking

Most beginners think:

> "I need to manually copy data."

People with **API thinking** think like this:

**Everything on the internet is a data source.**

If a website exists → there is usually an API.

And if there’s an API:

You can automate it.

Examples:

|System|API Use|
|---|---|
|Reddit|fetch posts|
|Notion|write database entries|
|Stripe|check payments|
|OpenAI|generate text|
|Google Calendar|create events|

Your automation becomes:

```
API → Process → API
```

Example of your Reddit workflow:

```
Reddit API
   ↓
n8n workflow
   ↓
Filter posts
   ↓
Notion API
   ↓
Save database
```

You just built a **data pipeline**.

---

# 4. The 4 API patterns you'll see everywhere

If you learn these, **80% of APIs will make sense**.

### GET

Get data.

Example:

```
GET /posts
```

Meaning:

> Give me posts.

---

### POST

Create something.

Example:

```
POST /tasks
```

Meaning:

> Create a new task.

---

### PUT / PATCH

Update something.

Example:

```
PATCH /task/123
```

Meaning:

> Update task 123.

---

### DELETE

Delete something.

Example:

```
DELETE /task/123
```

Meaning:

> Delete task 123.

---

# 5. What makes someone "API fluent"

When people become technical founders, they start seeing systems like this:

Instead of seeing apps:

```
Reddit
Notion
OpenAI
Stripe
```

They see:

```
Reddit API
Notion API
OpenAI API
Stripe API
```

And they think:

> What happens if I connect these?

That's literally how **most startups are built** now.

Example products:

|Product|APIs connected|
|---|---|
|Zapier|everything|
|n8n|everything|
|LangChain|LLM APIs|
|Many SaaS tools|Stripe + Auth + AI|

The modern internet is basically:

**APIs talking to APIs.**

---

# 6. Why this matters for YOU

You’re already doing things most beginners don't.

You already:

- built **n8n automation**
    
- call **Reddit JSON endpoint**
    
- send data to **Notion**
    
- design **workflow pipelines**
    

That is **API thinking in practice**.

The difference now is:

Before:

> I'm building a workflow.

After:

> I'm orchestrating APIs.

This mental shift is huge.

---

# 7. Best resources to learn API thinking

These are the **best beginner → advanced resources**.


### Postman API beginner guide

Very good practical explanation:

[https://learning.postman.com/docs/getting-started/introduction/](https://learning.postman.com/docs/getting-started/introduction/)

---

### FreeCodeCamp API course

Great tutorial:

[https://www.freecodecamp.org/news/what-is-an-api/](https://www.freecodecamp.org/news/what-is-an-api/)

---

### JSON guide (super important)

[https://www.json.org/json-en.html](https://www.json.org/json-en.html)

---

### REST API tutorial

[https://restfulapi.net/](https://restfulapi.net/)

---

# 8. If you want to go one level deeper

Next technical literacy topics that pair with APIs:

1️⃣ JSON parsing  
2️⃣ Authentication (API keys)  
3️⃣ Pagination  
4️⃣ Rate limits  
5️⃣ Webhooks

These are the **real API skills** builders use.

---

# 9. A small exercise (related to your Reddit workflow)

Open this:

```
https://www.reddit.com/r/startups/top.json?t=week&limit=5
```

Try to answer:

1️⃣ Where is the **title** field  
2️⃣ Where is **upvotes**  
3️⃣ Where is **comments**

If you can find those three things inside the JSON structure:

You officially understand **API + JSON reading**.

---

If you want, next I can also show you something **VERY useful for your automation journey**:

**The 5 API tricks builders use constantly**

(pagination, rate limits, webhooks, auth, idempotency)

Once you understand those, you basically unlock **technical founder literacy.**