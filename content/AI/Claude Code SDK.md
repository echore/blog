---
share: true
---
2026-04-13  21:43
Tags:[[Technical Literacy|Technical Literacy]]

## Claude Code SDK in simple terms:

It's a way to **control Claude Code programmatically** — instead of you typing to Claude manually, your own code talks to Claude Code.

---

## Normal Claude Code vs SDK:

**Normal Claude Code** — you type, Claude responds:

```
You: "add a verbose parameter to schema.ts"
Claude: *edits the file*
```

**Claude Code SDK** — your program talks to Claude:

```python
# Your script controls Claude automatically
result = claude.run("add a verbose parameter to schema.ts")
```

---

## Why would you want this?

Because you can **automate entire workflows:**

```python
# Instead of manually doing this every morning...
# 1. Open Claude Code
# 2. Type "review my code for bugs"
# 3. Type "write tests for new functions"
# 4. Type "update the README"

# You write a script that does all of it automatically:
claude.run("review my code for bugs")
claude.run("write tests for new functions")
claude.run("update the README")
```

---

## What you can do with it:

|Use case|What it means|
|---|---|
|**CI/CD pipelines**|Automatically have Claude review code on every git push|
|**Batch processing**|Run Claude on 100 files automatically|
|**Custom tools**|Build your own app that uses Claude Code under the hood|
|**Subagents**|Spin up multiple Claude instances working in parallel|

---

## How it relates to hooks:

Think of it this way:

```
Hooks  = react to what Claude does
SDK    = control what Claude does
```

Together they give you **full control** — you decide when Claude runs, what it does, and what happens at every step.

---

## Simple analogy:

- **Claude Code normally** = you driving a car manually
- **Claude Code SDK** = autopilot where your script drives the car
- **Hooks** = speed bumps and checkpoints along the road

---



Yes, you're absolutely right! You _can_ automate with scripts + cron. Great thinking. Here's the real difference:

## Regular scripts + cron:

You have to **know exactly what to do** in advance and hardcode every step:

```python
# You must predict every step
def morning_workflow():
    run("eslint src/")           # check linting
    run("pytest tests/")         # run tests
    run("git add . && git commit") # commit
```

What if linting fails? What if tests need fixing first? You have to code **every possible branch** yourself.

---

## Claude Code SDK:

Claude **thinks and adapts** — you just describe the goal:

```python
claude.run("make sure the codebase is clean and all tests pass")

# Claude figures out ON ITS OWN:
# → runs linting
# → sees 3 errors
# → fixes them
# → reruns linting
# → runs tests
# → sees a test failing
# → reads the error
# → fixes the code
# → reruns tests
# → all pass ✅
```

You didn't hardcode any of that logic. Claude reasoned through it.

---

## The core difference in one table:

||Scripts + Cron|Claude Code SDK|
|---|---|---|
|**Steps**|You define every step|Claude figures out steps|
|**Errors**|You handle every error case|Claude reads and fixes errors|
|**Flexibility**|Rigid, breaks on surprise|Adapts to unexpected situations|
|**Intelligence**|Zero|Can reason and problem-solve|

---

## Real analogy:

**Script + Cron** = a vending machine

- You press B3, it gives you chips
- Press wrong button → nothing happens
- Can't handle surprises

**Claude Code SDK** = a human assistant

- You say "get me a snack"
- They check what's available, figure it out, handle problems on their own

---

## So when would you still use plain scripts + cron?

When the task is **simple and predictable:**

- Back up a database every night → plain script is fine
- Send a weekly email report → plain script is fine
- Resize 1000 images → plain script is fine

Use Claude SDK when the task requires **judgment and reasoning:**

- Fix whatever bugs appeared today
- Review PRs and suggest improvements
- Refactor code to follow new patterns

---

Bottom line: **scripts follow instructions, Claude Code SDK thinks.** That's the real difference.




Exactly! You got it perfectly. Here are real examples:

## Scripts + Cron (predictable tasks):

```
✅ Back up database every night at 2am
✅ Send weekly sales report every Monday
✅ Resize all uploaded images to 800px
✅ Clear temp files every Sunday
✅ Check if website is down every 5 minutes
```

These are **always the same steps, zero thinking required.**

---

## Claude Code SDK (unknown/adaptive tasks):

### 1. Bug fixing after deployment

```
Scenario: Your app crashes in production at 3am

Script: ❌ Can't help — it doesn't know what broke

Claude SDK: ✅
→ reads the error logs
→ finds the broken file
→ understands the bug
→ fixes it
→ runs tests to confirm fix
→ commits the fix
```

### 2. Code review on every Pull Request

```
Scenario: Developer submits new code to GitHub

Script: ❌ Can only run linting/formatting rules you predefined

Claude SDK: ✅
→ reads the new code
→ understands what it's trying to do
→ spots logic errors scripts would miss
→ suggests better approaches
→ checks if it matches your coding style
→ leaves intelligent comments
```

### 3. Keeping documentation up to date

```
Scenario: Developer changes 10 functions this week

Script: ❌ Has no idea what changed or what the docs should say

Claude SDK: ✅
→ sees what code changed
→ reads the old documentation
→ understands what's now outdated
→ rewrites only the affected docs
→ keeps the same writing style
```

### 4. Migrating old code

```
Scenario: You want to upgrade from Python 2 → Python 3 across 200 files

Script: ❌ Can do simple find/replace but breaks on edge cases

Claude SDK: ✅
→ reads each file
→ understands the context
→ handles edge cases differently per file
→ runs tests after each migration
→ fixes whatever breaks
```

### 5. Onboarding new codebase

```
Scenario: You join a new company with a huge messy codebase

Script: ❌ Cannot help at all

Claude SDK: ✅
→ reads entire codebase
→ generates a clear explanation of how it works
→ draws architecture diagrams
→ answers your specific questions about it
```

---

## Summary:

|Task|Use|
|---|---|
|Same steps every time|Scripts + Cron|
|Needs reading & understanding|Claude SDK|
|Needs fixing unexpected errors|Claude SDK|
|Needs judgment & reasoning|Claude SDK|
|Simple, cheap, repetitive|Scripts + Cron|

The sweet spot is actually **combining both** — cron triggers Claude SDK only when intelligent work is needed, keeping costs low but adding power where it matters. 


## The idea:

```
Cron (scheduler) → checks a condition → if intelligent work needed → triggers Claude SDK
                                       → if simple/routine → handles it cheaply itself
```

Cron acts as a **gatekeeper** — only calling Claude (which costs money per use) when truly necessary.

---

## Why this matters:

Claude SDK costs money every time it runs. So you don't want it running on everything — only when thinking is actually required.

```
❌ Bad: Claude runs every 5 minutes on everything → expensive
✅ Good: Cron checks every 5 minutes, Claude only called when needed → cheap + smart
```

---

## Real Examples:

### 1. Customer Support Emails

```
Every 30 minutes, cron runs:

→ Are there new emails? 
   → No → do nothing, wait 30 min
   → Yes → are they simple? (order confirmation, password reset)
      → Yes → script sends template reply (cheap)
      → No → (complaints, complex questions) → trigger Claude SDK
                → Claude reads, understands, writes personal reply
```

### 2. Resume Screening

```
Every night at midnight, cron runs:

→ Did new resumes arrive today?
   → No → do nothing
   → Yes → how many?
      → Less than 5 → script saves them to a folder (human reviews manually)
      → More than 50 → trigger Claude SDK
                → Claude reads all, ranks them, delivers shortlist
```

### 3. Social Media Monitoring

```
Every hour, cron runs:

→ Any new mentions of our brand?
   → No → do nothing
   → Yes → what kind?
      → Positive comments → script auto-likes them (cheap)
      → Negative/angry → trigger Claude SDK
                → Claude reads the complaint
                → understands the context
                → writes thoughtful response
```

### 4. Financial Anomaly Detection

```
Every morning at 9am, cron runs:

→ Check yesterday's transactions
   → All normal? → script generates routine report (cheap)
   → Something unusual? (big spike, sudden drop) → trigger Claude SDK
                → Claude analyzes what happened
                → compares with historical patterns
                → writes explanation for management
```

### 5. Content Moderation

```
Every 10 minutes, cron runs:

→ New user posts on platform?
   → No → do nothing
   → Yes → run simple keyword filter first (cheap)
      → Clearly fine → approve automatically
      → Clearly bad (known slurs etc) → script auto-removes (cheap)
      → Unclear/borderline → trigger Claude SDK
                → Claude reads full context
                → makes intelligent judgment call
```

---

## The decision tree in every example is the same:

```
Cron triggers
      ↓
Is there anything to do?
   → No → stop, save money
   → Yes → is it simple and predictable?
      → Yes → handle with cheap script
      → No → call Claude SDK for intelligence
```

---

## Cost comparison example:

```
Customer support — 1000 emails per day

❌ Claude handles all 1000:
   1000 × $0.01 = $10/day = $300/month

✅ Script filters first:
   700 simple emails → script handles free
   300 complex emails → Claude handles
   300 × $0.01 = $3/day = $90/month

Savings: 70% cheaper, same quality
```

---

## One sentence summary:

**Cron is the cheap watchman who checks constantly, and only calls the expensive expert (Claude) when the situation actually needs intelligence.**



Yes! basically that's the idea. You create a script file (could be `sdk.ts` or any name) and use the Claude Code SDK inside it.

## Basic structure:

```typescript
// sdk.ts
import Anthropic from "@anthropic-ai/sdk";

const client = new Anthropic();

const response = await client.messages.create({
  model: "claude-sonnet-4-20250514",
  max_tokens: 1000,
  messages: [
    { role: "user", content: "review my code for bugs" }
  ]
});

console.log(response);
```

---

## But actually Claude Code SDK is slightly different:

It's not just the Anthropic API — it's specifically for **running Claude Code programmatically**, meaning Claude can actually use tools, edit files, run commands etc.

```typescript
// sdk.ts
import { ClaudeCode } from "@anthropic-ai/claude-code";

const result = await ClaudeCode.run({
  prompt: "find all bugs in src/ and fix them",
  workingDirectory: "./my-project"
});
```

---

## So the file naming is flexible:

```
sdk.ts          ✅ fine
automation.ts   ✅ fine  
workflow.ts     ✅ fine
morning-job.ts  ✅ fine
```

Name it whatever describes **what the script does.**

---

