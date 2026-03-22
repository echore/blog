---
share: true
---
2026-03-22  17:24
Tags:[[Technical Literacy|Technical Literacy]]

https://youtu.be/7j1t3UZA1TY?si=x4iersxriU7AXcNu


---

# Model Context Protocol (MCP) vs APIs

## 1. Why MCP exists

For large language models (LLMs) to be truly useful, they must:

- Access external data (documents, databases, knowledge bases)
    
- Use tools (APIs, services, actions)
    

Traditionally, this was done using **APIs**.

However, APIs were not designed specifically for AI agents.

→ This led to the introduction of **Model Context Protocol (MCP)** in late 2024 by Anthropic.

---

## 2. What is MCP

**Definition:**

> **MCP is an open standard protocol that standardizes how applications provide context and tools to LLMs.**

---

## 3. Core Analogy (important)

MCP can be understood as:

> **USB-C for AI systems**

### Mapping:

|Real World|MCP Equivalent|
|---|---|
|Laptop|MCP Host|
|USB-C Port|MCP Protocol|
|External devices (monitor, disk, power)|MCP Servers|

Key idea:

- Different tools/services can connect using the same standard
    
- It does not matter who built them
    
- Everything works together through a unified interface
    

---

## 4. MCP Architecture

MCP follows a **client–server model**.

### Components:

- **MCP Host**
    
    - Runs the AI application
        
- **MCP Client**
    
    - Opens a session using MCP protocol (JSON-RPC 2.0)
        
    - Communicates with servers
        
- **MCP Server**
    
    - Exposes capabilities (tools, data, prompts)
        

---

### Flow:

```text
LLM / Agent
   ↓
MCP Client
   ↓ (JSON-RPC)
MCP Server
   ↓
External systems (DB, APIs, services)
```

---

## 5. What MCP Enables

MCP solves two core needs of AI agents:

### 1. Context Retrieval

Access external data:

- documents
    
- database records
    
- knowledge bases
    

---

### 2. Tool Usage

Execute actions:

- web search
    
- API calls
    
- calculations
    
- system operations
    

---

## 6. MCP Primitives (Core Concepts)

MCP servers expose **three main primitives**:

---

### 6.1 Tools

**Definition:**  
Discrete actions the AI can execute

Examples:

- `get_weather`
    
- `create_event`
    

Characteristics:

- Defined with name, description, input/output schema
    
- Executed by server when invoked
    

---

### 6.2 Resources

**Definition:**  
Read-only data provided by the server

Examples:

- text files
    
- database schema
    
- documents
    

Used for:

- providing context to the model
    

---

### 6.3 Prompt Templates

**Definition:**  
Predefined prompt structures

Purpose:

- guide model behavior
    
- standardize interactions
    

---

### Important Insight

- Not all servers implement all primitives
    
- Many focus primarily on **tools**
    

---

## 7. Dynamic Discovery (Key Advantage)

MCP supports:

> **Runtime capability discovery**

Meaning:

- Agent can ask:
    
    > “What can you do?”
    
- Server returns:
    
    - available tools
        
    - resources
        
    - prompts
        

---

### Implication:

- No need to hardcode integrations
    
- No redeployment required when capabilities change
    
- Agents adapt dynamically
    

---

## 8. What is an API

**Definition:**

> An API (Application Programming Interface) defines how one system can request data or services from another.

---

### Key Characteristics:

- Defines request/response structure
    
- Abstracts internal implementation
    
- Enables system integration
    

---

### Example Use Case:

- E-commerce → payment API
    
- AI → web search API
    

---

## 9. REST API (Most Common Type)

REST APIs operate over HTTP.

### Common Methods:

|Method|Purpose|
|---|---|
|GET|Retrieve data|
|POST|Create data|
|PUT|Update data|
|DELETE|Remove data|

---

### Example:

```text
GET /books/123
POST /loans
```

Responses are typically in **JSON format**.

---

## 10. Similarities Between MCP and APIs

Both:

- Use **client–server architecture**
    
- Provide **abstraction layers**
    
- Hide internal implementation details
    
- Enable system integration
    

---

### Comparison Flow:

|MCP|REST API|
|---|---|
|Client → MCP Server|Client → API Server|
|tools/call|HTTP request|
|structured response|JSON response|

---

## 11. Key Differences

### 11.1 Purpose

|MCP|API|
|---|---|
|Designed for AI agents|General-purpose|
|Focus on context + tools|Focus on data/services|

---

### 11.2 Dynamic Discovery

|MCP|API|
|---|---|
|Built-in capability discovery|Usually none|
|Agent adapts automatically|Requires manual updates|

---

### 11.3 Standardization

|MCP|API|
|---|---|
|Unified interface|Each API is different|
|Same structure across servers|Different endpoints, formats|

---

### Key Insight:

> MCP = "build once, integrate many"  
> API = "integrate separately each time"

---

## 12. Relationship Between MCP and APIs

Very important:

> MCP does NOT replace APIs  
> MCP builds on top of APIs

---

### How they work together:

- MCP Server = wrapper layer
    
- Internally calls traditional APIs
    

---

### Example:

MCP GitHub Server:

- Exposes:
    
    - `repository/list` (MCP tool)
        
- Internally:
    
    - Calls GitHub REST API
        

---

### Conclusion:

> MCP and APIs are **layers in the same system**

```text
AI Agent
   ↓
MCP (standard interface)
   ↓
API (actual execution)
   ↓
External service
```

---

## 13. Why MCP Matters

MCP enables:

- standardized integration for AI agents
    
- dynamic tool usage
    
- reduced engineering overhead
    
- scalable system design
    

---

### Real-world MCP integrations:

- file systems
    
- Google Maps
    
- Docker
    
- Spotify
    
- enterprise data systems
    

---

## 14. Key Takeaways

1. MCP standardizes how AI interacts with tools and data
    
2. It introduces dynamic discovery and unified interfaces
    
3. It simplifies multi-system integration
    
4. It works on top of existing APIs, not instead of them
    

---

## One-line summary

> MCP is a standardized interface layer that allows AI agents to discover, access, and use tools and data dynamically, often by leveraging APIs underneath.