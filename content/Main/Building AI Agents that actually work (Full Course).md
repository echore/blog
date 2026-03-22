---
share: true
---
2026-03-22  16:48
Tags:[[Technical Literacy|Technical Literacy]]
https://youtu.be/eA9Zf2-qYYM?si=shppP2vQoOT5oWej
really great video

---

# AI Agents: Structured Summary

## 1. From Chat Models to Agents

A key shift in AI usage is moving from **chat-based interaction** to **agent-based execution**:

- **Chat model:** Question → Answer
    
- **Agent:** Goal → Result
    

Chat models require continuous user input and back-and-forth interaction.  
Agents, by contrast, take a goal, plan the steps, execute them, and deliver a final outcome.

---

## 2. The Agent Loop

At the core of every agent is a continuous loop:

- **Observe** (gather context and information)
    
- **Think** (decide what to do next)
    
- **Act** (execute the step)
    

This loop repeats until the task is complete.

Unlike chat models, agents do not stop after one response. They iterate autonomously until they reach the defined objective.

---

## 3. Key Components of an Agent

An AI agent consists of four main elements:

1. **LLM (Large Language Model):** the reasoning engine
    
2. **Loop:** enables continuous execution until completion
    
3. **Tools:** external integrations (e.g., browser, APIs, apps)
    
4. **Context:** structured information about the user, task, and environment
    

Agent platforms (called “agent harnesses”) provide the infrastructure to connect these components.

---

## 4. Context Engineering vs Prompt Engineering

There is a shift from:

- **Prompt engineering** → crafting better instructions  
    to
    
- **Context engineering** → structuring the environment in which the agent operates
    

Instead of writing complex prompts, users define:

- Role (e.g., executive assistant, marketing lead)
    
- Business context
    
- Preferences
    
- Available tools
    

This allows simple prompts (e.g., “write a cold email”) to produce high-quality outputs.

---

## 5. Agent Memory

Unlike chat models, agents do not automatically remember user preferences across sessions.

To address this, users create structured memory files:

- **agents.md / claude.md:** defines role and persistent context
    
- **memory.md:** stores learned preferences over time
    

This enables agents to:

- Learn from corrections
    
- Retain user-specific preferences
    
- Improve performance across sessions
    

Memory compounds over time, similar to training an employee.

---

## 6. Skills (AI SOPs)

Skills are reusable procedures that encode workflows:

- Defined as structured markdown files
    
- Represent repeatable processes (SOPs)
    
- Allow the agent to execute tasks consistently without re-instruction
    

Example use cases:

- Writing proposals
    
- Generating marketing content
    
- Analyzing competitors
    
- Sending structured emails
    

Skills can be created in two ways:

1. From existing knowledge (e.g., transcripts, courses)
    
2. From past interactions (convert a completed workflow into a reusable skill)
    

---

## 7. MCP (Model Context Protocol)

MCP enables agents to interact with external tools.

It acts as a universal translator between:

- The LLM (which uses natural language)
    
- Tools (which use different technical formats)
    

This allows agents to:

- Access Gmail, Notion, Calendar, Stripe, etc.
    
- Perform multi-step workflows across platforms
    
- Execute real-world tasks beyond text generation
    

---

## 8. From Tasks to Systems

The overall paradigm shift is:

- From executing isolated tasks
    
- To building integrated systems
    

Users are encouraged to:

- Define roles (e.g., executive assistant, marketing lead)
    
- Provide structured context
    
- Connect tools
    
- Build skills over time
    

As these components accumulate, agents evolve into a personalized **AI operating system** that manages workflows across different domains.

---

## 9. Compounding Productivity

The main advantage of agents is compounding efficiency:

- Automating small repetitive tasks
    
- Converting workflows into reusable skills
    
- Reducing manual tool-switching
    
- Enabling parallel and continuous execution
    

Over time, this leads to:

- Significant time savings
    
- Increased output
    
- Higher leverage in both personal and professional work
    

---

## 10. Practical Implementation Approach

A recommended progression:

1. Start with a simple agent (e.g., executive assistant)
    
2. Define context (role, preferences, tools)
    
3. Add memory for personalization
    
4. Build skills from repeated tasks
    
5. Connect tools via MCP
    
6. Gradually expand into multiple agents (by function or department)
    

---

## Conclusion

AI agents represent a shift from interaction-based AI to execution-based AI.

The key idea is not to “use AI tools,” but to:

- Design systems
    
- Structure context
    
- Encode workflows
    
- Build autonomous processes
    

This transforms AI from a helper into an operational layer capable of managing complex tasks independently.