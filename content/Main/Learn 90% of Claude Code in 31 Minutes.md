---
share: true
---
2026-03-27  14:51
Tags:
https://youtu.be/TwkdDcO4vWQ?si=gQNbzBZa1qRwXQfQ
## Conslusion:
* give it full permission (well~)
* good prompts contains: 
	* you specific goal
	* give it example
	* always ask open questions if you were an expert in xx what do you think
* always have plan mode
* don't just accept the recommendation, if you don't understand what they are doin, ask it, learn it! you need to know, you need to give it direction!
* use the skill! it can be better
* Context Window Management
* [[CLI|CLI]] is good 


它甚至可以自己测试app，功能对不对。。。。
还可以直接告诉它commit and push to github....
推荐下载github cli and vercel cli 更新的话就告诉它commit and push to github.可以自动github and vercel都更新好。。。


## In the terminal (main way)

When Claude Code is running, press **`Shift+Tab`** to cycle through permission modes:

- **Auto-accept edits** — Claude makes file changes without asking
- **Plan mode** — Claude describes what it _would_ do but asks before every action
- **Default** — Claude asks permission for risky actions (file writes, shell commands)



# 3. Permissions System (Core Mechanism)

Claude Code operates with different permission levels, which determine how autonomously it can act.

---

## Permission Levels

### Default Mode

- Claude asks for permission before every action
    
- Includes file edits, command execution, etc.
    
- Extremely slow and interruptive
    

---

### Accept Edits Mode

- Claude can edit files without asking
    
- Still asks for permission before running system-level commands (e.g., installing tools)
    

This is the recommended starting point.

---

### Bypass Permissions Mode

Enabled via:

```bash
claude --dangerously-skip-permissions
```

This allows Claude to:

- Modify files freely
    
- Execute commands freely
    
- Install tools, run scripts, etc.
    

---

## Trade-off

- More autonomy → faster workflow
    
- Less control → higher risk
    

The transcript notes that most experienced users eventually move to bypass mode because:

> Constant permission prompts destroy productivity.

---

# 4. The Most Important Skill: Prompting

The transcript emphasizes that prompting is not just important—it is the **central skill**.

---

## Problem with Naive Prompting

Example:

> “Build a kanban board”

This leads to:

- Generic output
    
- Missing features
    
- Poor design decisions
    

Because:

- Claude fills in gaps arbitrarily
    

---

## High-Quality Prompt Structure

### 1. Define the Goal (Not Just the Task)

Instead of:

> Build a kanban board

You define:

- Why the board exists
    
- What it is supposed to enable
    

Example:

- Organize past and future content
    
- Track performance
    
- Plan upcoming work
    

---

### 2. Provide Examples

Claude performs significantly better when given:

- Screenshots (UI inspiration)
    
- GitHub repositories
    
- Concrete references
    

This reduces ambiguity.

---

### 3. Ask Open-Ended Expert Questions

This is one of the most important insights in the transcript.

You explicitly ask:

- What am I missing?
    
- What would an expert consider?
    
- What are potential unintended consequences?
    

---

## Why This Matters

AI enables you to operate in domains where you lack expertise. However:

> You do not know what you do not know.

Therefore:

- Claude must help fill those blind spots
    
- But only if you explicitly ask
    

---

# 5. Plan Mode (Critical for Better Output)

Plan mode changes Claude’s behavior from:

> “Execute immediately”

to:

> “Clarify before executing”

---

## Without Plan Mode

Claude:

- Makes assumptions
    
- Starts building immediately
    
- Produces average results
    

---

## With Plan Mode

Claude:

- Asks clarifying questions
    
- Forces you to define:
    
    - Features
        
    - structure
        
    - constraints
        

---

## Key Insight

Plan mode is not just a feature.

It is a mechanism that forces **thinking before execution**, which is essential for non-technical users.

---

# 6. The Learning Trap (Very Important Section)

You can't just accept, if you don't understand , ask it!

---

# 7. Skills (How to Improve Claude’s Output)

Skills are described as:

> Text prompts that modify how Claude performs tasks.

---

## Two Types of Skills

### 1. Performance Skills

- Improve quality of outputs
    
- Example: frontend design skill
    

---

### 2. Workflow Skills

- Combine multi-step processes into one command
    
- Increase efficiency
    

---

## Key Limitation of AI

Claude struggles with:

- Taste
    
- Design judgment
    
- Creative decisions
    

---

## Example: Frontend Design

Without skill:

- Generic UI
    
- “AI-looking” output
    

With skill:

- Improved layout
    
- Better aesthetics
    
- More refined design
    

---

## Important Clarification

Skills are:

- Not automatic
    
- Must be invoked explicitly or implicitly
    

Methods:

- Slash command (guaranteed trigger)
    
- Natural language (probabilistic trigger)
    

---

# 8. Context Window Management (Performance Control)

Claude has a limited context window (~1 million tokens).

---

## What Are Tokens?

- Roughly equivalent to words
    
- Includes:
    
    - input
        
    - output
        
    - tool usage
        
    - skill usage
        

---

## Problem: Context Rot

As context grows:

- Performance degrades
    
- Accuracy decreases
    
- Outputs become worse
    

---

## Observed Threshold

Around 20% of context capacity:

- noticeable performance drop begins
    

---

## Solution: Reset Context

Command:

```bash
/clear
```

This:

- wipes conversation memory
    
- keeps access to project files
    

---

## Why This Works

Claude can:

- re-read files from the project
    
- reconstruct context when needed
    

---

## Best Practice

- Keep sessions short
    
- Reset frequently
    
- Avoid unnecessary accumulation
    

---

## Additional Tool

```bash
/context
```

Allows you to:

- monitor token usage
    

---

# 9. CLI Tools (Major Capability Expansion)

CLI = Command Line Interface tools that run in the terminal.

---

## Why CLI Matters

Claude runs in the terminal.

Therefore:

- it can directly control CLI tools
    
- without heavy overhead
    

---

## Benefits

- Lower token usage
    
- Faster execution
    
- More reliable workflows
    

---

## Example: Supabase

Instead of manually:

- creating database
    
- configuring auth
    

You can:

- ask Claude to do it via CLI
    

---

## Example: Playwright

Playwright CLI enables:

- browser automation
    
- UI testing
    

Claude can:

- open browser
    
- simulate user actions
    
- validate behavior
    

---

## Key Insight

CLI transforms Claude from:

- assistant → operator
    

---

# 10. Automated Testing (Practical Application)

Using Playwright CLI:

Claude can:

- generate test cases
    
- execute them
    
- simulate real user behavior
    

---

## Example Actions

- Create cards
    
- Move elements
    
- Verify UI behavior
    
- Check interactions
    

---

## Advanced Detail

“Headed browsers”:

- visible browser windows
    
- useful for debugging
    

vs

“Headless”:

- runs in background
    
- faster
    

---

# 11. Deployment Workflow (From Local to Public)

The transcript outlines a simple pipeline:

---

## Step 1: GitHub

Commands:

- commit → save locally
    
- push → upload to GitHub
    

Claude can automate this.

---

## Step 2: Vercel

- Connect GitHub repository
    
- Deploy project
    
- Get public URL
    

---

## System Flow

Claude Code → GitHub → Vercel → Live Website

---

## Key Feature

- Automatic redeployment
    
- Every push triggers update
    

---

## Error Handling

If deployment fails:

- copy error
    
- paste into Claude
    
- Claude fixes it
    

---

# 12. The Four Core Levers (Final Synthesis)

The transcript ultimately identifies four ways to improve results:

---

## 1. Prompting

Defines:

- what you want
    
- why you want it
    

---

## 2. Skills

Improves:

- how Claude executes
    

---

## 3. Context Management

Controls:

- performance quality over time
    

---

## 4. CLI Tools

Expands:

- what Claude is capable of doing
    

---

# 13. Final Meta Insight

The most important conceptual takeaway:

Claude Code does not replace thinking.

---

## It enables:

- non-technical users to build
    
- faster execution
    
- broader exploration
    

---

## But differentiation comes from:

- problem definition
    
- judgment
    
- taste
    
- decision-making
    

---

## Critical Warning

If you:

- always accept defaults
    
- never understand tools
    

Then:

- you become indistinguishable from anyone else using Claude
    

---

## Real Role of the User

You are not coding.

You are:

- directing
    
- deciding
    
- refining
    

---

If you want, next step I can do something much more useful for your situation:

→ map this directly to **how you should use Claude Code for your startup / job / portfolio building**

That’s where this actually becomes powerful for you.