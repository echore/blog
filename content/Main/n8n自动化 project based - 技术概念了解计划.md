---
share: true
---
2026-03-07  14:05
Tags:[[Technical Literacy|Technical Literacy]]

你现在这个 **Reddit → n8n → Notion 自动化**其实是一个非常好的“技术素养训练场”。不是去学一堆抽象 CS，而是把一个真实系统拆开看。  
我给你讲几个**最值得顺手提高 Technical Literacy 的方向**，而且都是你这个项目里已经在碰到的东西。

---

# 1️⃣ API 思维（最核心）
A full API request usually has:

**METHOD + URL + PARAMETERS + HEADERS (authentication) + RESPONSE (JSON)**

You already know the **method** part, so let’s fill in the rest.

你现在已经在做：

HTTP Request → Reddit API

接下来你可以理解更深一点的几个点：

### API 的基本结构

几乎所有 API 都有：

- **Endpoint**
    
    ```
    https://www.reddit.com/r/.../top.json
    ```
    
- **Parameters**
    
    ```
    ?t=week&limit=10
    ```
    
- **Headers**  
    比如 user-agent / auth
    
- **Response**
    

理解这些，你以后就能：

- 接 Notion API
    
- 接 OpenAI API
    
- 接 Stripe
    
- 接任何 SaaS
    

这就是 **现代软件世界的通用语言**。

Yeah — that reaction is **completely normal**. APIs look small at first, then suddenly you realize **there’s a whole world behind them**. You're not wrong calling it a _huge object_. It really is a big ecosystem.

But here's something important that most beginners miss:

> **You do not need to understand the whole API world to use APIs effectively.**

Especially for what you're doing (automation, data pipelines, products). Let me zoom out a bit so the landscape feels less overwhelming.

---

## 1. The API world actually has layers

What you saw on YouTube probably mixed **many layers together**.

Think of APIs like a **stack**.

### Layer 1 — Basic usage (what you're doing now)

This is **90% of practical work**.

You only need to understand:

- HTTP methods
    
- URLs / endpoints
    
- JSON responses
    
- authentication (API keys)
    
- request parameters
    

Example:

```
GET https://api.reddit.com/r/financialindependence/top.json
```

Response:

```
JSON → parse → send to Notion
```

This is exactly what your **n8n workflow** does.

You’re already here.

---

### Layer 2 — API design

This is what backend engineers think about:

- REST architecture
    
- resource modeling
    
- versioning
    
- pagination
    
- rate limits
    

Example:

```
GET /posts?page=2&limit=20
```

This is useful **if you build APIs**, not just consume them.

---

### Layer 3 — API infrastructure

This is deeper engineering:

- API gateways
    
- authentication systems
    
- caching
    
- load balancing
    
- distributed systems
    

Companies like:

- Stripe
    
- AWS
    
- Google
    
- Netflix
    

spend **millions designing these systems**.

But most developers never touch this.

---

## 2. The mental model that simplifies APIs

Instead of thinking “API is huge”, think:

> **API = remote function call over the internet**

Example:

Local function in Python:

```
get_user(id=42)
```

API call:

```
GET /users/42
```

Same idea — just across the network.

---

## 3. The surprising truth

The **entire internet economy runs on APIs**.

Examples:

Stripe payment

```
POST /charges
```

OpenAI

```
POST /chat/completions
```

Notion

```
POST /pages
```

Reddit

```
GET /top.json
```

Everything is basically:

```
service → API → service → API
```

---

## 4. What matters for _your path_

Given what you're doing (automation + product thinking), the **useful API knowledge** is actually small.

You only need to deeply understand these **5 things**:

1️⃣ **HTTP requests**

```
GET
POST
PATCH
DELETE
```

2️⃣ **JSON structure**

```
{
 "title": "post",
 "score": 123
}
```

3️⃣ **authentication**

```
Authorization: Bearer API_KEY
```

4️⃣ **parameters**

```
?limit=10&sort=top
```

5️⃣ **webhooks**

Event-based APIs.

---

## 5. The funny part: you already crossed the hardest step

Most people never reach the stage where they:

- read API docs
    
- parse JSON
    
- build automation workflows
    

But you already did this with:

- Reddit API
    
- Notion API
    
- n8n pipelines
    

That means your **technical literacy is already growing**.

---

## 6. The learning strategy that works best

Instead of studying APIs in theory, do what you're already doing:

> **Learn APIs through projects.**

Example path:

1️⃣ Reddit → Notion automation  
2️⃣ Add OpenAI summarization  
3️⃣ Add webhook triggers  
4️⃣ Store data in a database  
5️⃣ Build a small web dashboard

Each project adds **one concept**.

---

## 7. The comforting truth

Even senior engineers **don't know the whole API world**.

They just know how to quickly answer:

```
What endpoint?
What method?
What parameters?
What JSON comes back?
```

Once you can answer those four questions, you can use almost any API.

---

If you want, I can also show you something that will **make APIs feel much smaller**:

There are actually only **about 7 core API patterns** that almost every company uses (Reddit, Stripe, OpenAI, Notion, Shopify, etc.).

Once you recognize those patterns, reading API docs becomes _way easier_.

---

# 2️⃣ JSON 结构阅读能力

你现在看到 JSON 应该越来越熟悉了：

```
data
 └ children
     └ data
        └ title
```

你可以顺手练几个技能：

### JSON path 思维

比如：

```
$data.children[0].data.title
```

### 判断结构

这是：

```
object
array
object
```

### 提取字段

title  
ups  
num_comments  
permalink

这其实是 **数据工程的基础能力**。

---

# 3️⃣ 数据库设计（超级关键）

你现在其实已经在做一个 **小数据产品**。

你的 Notion Database 就是数据库。

你可以开始想：

### 一个帖子需要哪些字段？

你现在有：

- Title
    
- Subreddit
    
- Upvotes
    
- Comments
    
- URL
    
- Week
    
- Permalink
    
- Status
    
- Depth
    

你可以问自己：

**哪些字段是唯一ID？**

答案其实是：

```
Permalink
```

这就是为什么我们用它去重。

这其实就是：

### 数据库概念

- primary key
    
- unique id
    
- schema design
    

这比很多人写代码都更重要。

---

# 4️⃣ 去重逻辑（真实工程思维）

你现在已经遇到了一个很真实的问题：

**同一帖子会被抓到很多次**

所以你用了：

```
Permalink 去重
```

你可以进一步理解：

### 去重的三种方式

**1 数据库层**

```
unique permalink
```

**2 workflow层**

n8n先查Notion

如果存在 → skip

**3 hash去重**

比如：

```
hash(title + url)
```

这是很多 ETL pipeline 的核心逻辑。

---

# 5️⃣ Automation Workflow 设计

你现在其实在做一个 **data pipeline**。

结构大概是：

```
Schedule
   ↓
HTTP Request
   ↓
Split Items
   ↓
Filter (去 discussion)
   ↓
Transform fields
   ↓
Dedup
   ↓
Database (Notion)
```

这就是：

### ETL Pipeline

E → Extract  
T → Transform  
L → Load

你已经在做 **数据工程入门**。

---

# 6️⃣ Debug 能力

你这几天其实已经在练这个了：

比如：

- 为什么 JSON 不对
    
- IF 条件为什么不触发
    
- sticky 帖子怎么过滤
    
- split items 怎么用
    

真正工程师每天都在干这个：

```
看 log
看 response
改条件
再跑
```

这是 **工程思维**。

---

# 7️⃣ Web 基础（你可以顺便理解）

这个项目还会让你自然理解：

### HTTP

```
GET
POST
```

### URL结构

```
domain
path
query params
```

### status code

```
200
404
429
```

这些都是互联网底层语言。

---

# 8️⃣ 数据产品思维（其实很重要）

你现在抓 Reddit 数据，其实是在做：

**content intelligence system**

以后你完全可以：

抓：

- Reddit
    
- HackerNews
    
- Twitter
    
- YouTube
    

然后：

```
自动分析
自动总结
自动选题
自动写内容
```

这就是很多 AI 产品在做的事情。

---

# 9️⃣ AI integration（下一步）

等你 pipeline 稳定了，你可以加：

```
Reddit
  ↓
Filter
  ↓
AI summarize
  ↓
AI classify
  ↓
Notion
```

比如：

```
Depth score
Topic
Hook
Summary
```

这就是 AI workflow。

---

# 🔟 最重要的一点

你现在学到的不是：

**coding**

而是：

**how systems talk to each other**

这是很多 founder 才有的能力。

你现在其实已经在理解：

- API
    
- data pipeline
    
- schema
    
- automation
    
- AI integration
    

这就是 **technical literacy**。

---

我其实很好奇一件事：

你现在做完这个 Reddit automation，  
**你脑子里有没有开始出现这种感觉：**

> 原来互联网很多东西，本质就是
> 
> “抓数据 → 处理 → 存储 → 再利用”

如果你有这种感觉，说明你的 **技术视角已经开始建立了。**