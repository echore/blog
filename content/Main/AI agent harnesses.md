---
share: true
---
2026-03-27  11:27
Tags:[[Technical Literacy|Technical Literacy]]


**What is an agent harness?**

The term "harness" borrows from horse tack — reins, saddle, bit — the complete set of equipment for channeling a powerful but unpredictable animal. The AI model is the horse: powerful and fast, but without direction. The human engineer is the rider. Without a harness, an AI agent is a thoroughbred in an open field: fast, impressive, and useless for getting anything done.

More precisely, harness engineering is the discipline of designing the systems, constraints, and feedback loops that wrap around AI agents to make them reliable in production. A harness is not the agent itself — it's the complete infrastructure that governs how the agent operates: the tools it can access, the guardrails that keep it safe, the feedback loops that help it self-correct, and the observability layer that lets humans monitor its behavior.

Here's a visual overview of the key layers:**Why does it matter so much right now?**
![[Pasted image 20260327112808.png|Pasted image 20260327112808.png]]

The core challenge of long-running agents is that they must work in discrete sessions, and each new session begins with no memory of what came before. Imagine a software project staffed by engineers working in shifts, where each new engineer arrives with no memory of what happened on the previous shift.

The uncomfortable truth the AI industry is confronting: the underlying model matters less than the system around it. LangChain proved this definitively — their coding agent jumped from Top 30 to Top 5 on a benchmark by changing nothing about the model, only the harness around it.

**The key components of a harness**

**Context engineering** is about what the agent can "see." From the agent's point of view, anything it can't access in-context while running effectively doesn't exist. Knowledge that lives in Google Docs, chat threads, or people's heads is inaccessible. Repository-local, versioned artifacts — code, markdown, schemas — are all it can see.

**Architectural constraints** keep the agent consistent. OpenAI enforces architectural boundaries and dependency layers through mechanical rules and structural tests. Dependencies flow in a controlled sequence, with agents restricted to operate within these layers. Structural tests validate compliance and prevent violations of modular layering.

**Garbage collection** combats drift. Full agent autonomy introduces novel problems: agents replicate patterns that already exist in the repository — even uneven ones — inevitably leading to drift. OpenAI started encoding "golden principles" directly into the repository and built a recurring cleanup process: opinionated, mechanical rules that keep the codebase legible and consistent for future agent runs.

**Human-in-the-loop controls** are placed strategically. Harnesses include designing when and how humans are consulted — from explicit approval gates ("the agent wants to delete a database — approve?") to periodic review checkpoints. The goal is not micromanagement, but placing human judgment at high-leverage decision points where the cost of a mistake is highest.
