---
share: true
---
2026-03-29  13:01
Tags:[[Technical Literacy|Technical Literacy]]


## My global md
**Open the file directly in Finder:**

```bash
open ~/.claude/
```

This opens the `.claude` folder in Finder, then you can double-click `CLAUDE.md` to open it in any editor.

```
# My Global Preferences

## Workflow
- Always start in plan mode — break down the task into steps before doing anything
- Show me the plan and wait for my approval before executing
- Always initialize git at the start of every new project
- Always commit the current state before making any edits or deletions

## Permissions
- Adding new code or files: go ahead without asking
- Editing existing code: ask me first and explain what you're changing and why
- Deleting anything: NEVER delete without explicitly asking me first and waiting for confirmation

## Git Commits
- Use clear commit messages that describe what changed and why
- Keep commits small and focused on one change at a time
```


https://kirill-markin.com/articles/claude-code-rules-for-ai/
This one is really great!
## Global CLAUDE.md First, Project CLAUDE.md Second

I do not want one giant `CLAUDE.md` with everything jammed into it.

My global file should answer questions like:

- How strict should typing be?
- How do I want errors handled?
- Do I want minimal diffs or broad refactors?
- What kind of documentation do I expect?

My project file should answer different questions:

- How do I run the project?
- Which commands are safe and expected?
- What are the important architecture boundaries?
- Where do tests live?
- Which conventions are specific to this repo only?

In practice:

- global `CLAUDE.md` says how I work
- project `CLAUDE.md` says how this repo works

## My Practical Rollout for Claude Code Rules

If I were setting this up from scratch today, I would do it in this order.

### 1. Create `~/.claude/CLAUDE.md`

Start with your non-negotiables. Not life advice. Not engineering manifestos. Just the rules that repeatedly matter across repositories.

For me, that means:

- strict typing
- explicit error handling
- minimal edits
- no silent fallbacks
- docstrings where documentation belongs
- non-interactive terminal habits

That alone already changes the output more than most prompt tweaks.

### 2. Add a Project `CLAUDE.md`

Use the repo file for commands, architecture, naming, and boundaries. Anthropic gives you `/init` to draft one, which is useful. I still edit it manually after that because generated instructions are a draft, not a finished artifact.

### 3. Keep Project Rules Short

Do not turn the project file into a second copy of your personal one. Put repo-specific commands, architecture notes, and local conventions there. Leave your durable preferences in the global file.




https://dometrain.com/blog/creating-the-perfect-claudemd-for-claude-code/
for project specific claude.md
## What to Put Inside the CLAUDE.md File
#### Terminal Commands
#### Workflows
#### Coding Standards and Styles
#### Domain-Specific Jargon
#### Architectural Decisions and Structure
#### Model Context Protocol (MCP) Instructions



## When I start a new project is it better for me to create a claude md first?

---

**Option A: Write it first (spec-driven)**

Before coding, write a CLAUDE.md that describes what you're building:

- What the project does
- Tech stack you plan to use
- Folder structure you want
- Key conventions

Then Claude Code starts with full context from day one. Good if you already know what you're building.

---

**Option B: Run `/init` after the first setup (most common)**

1. Start coding / scaffolding with Claude
2. Once basic structure exists, run `/init`
3. Review and add anything it missed
4. Keep updating it as the project evolves

This is what most people do because you often don't know all the details upfront.

---

**The most important habit either way:**

Treat CLAUDE.md as a **living document**. Whenever Claude makes a mistake that better context would have prevented — add it to the file. For example:

- Claude used `npm` but you use `bun` → add it
- Claude restructured something you didn't want touched → add a note
- Claude forgot your naming convention → add it

Over time it gets smarter about your specific project.

---

Given how well your search workflow CLAUDE.md turned out, I'd say **Option B fits your style** — let `/init` do the heavy lifting, then refine it. You clearly know what details matter to add! 👍


https://www.humanlayer.dev/blog/writing-a-good-claude-md

##  In Conclusion

1. `CLAUDE.md` is for onboarding Claude into your codebase. It should define your project's **WHY**, **WHAT**, and **HOW**.
2. **Less (instructions) is more**. While you shouldn't omit necessary instructions, you should include as few instructions as reasonably possible in the file.
3. Keep the contents of your `CLAUDE.md` **concise and universally applicable**.
4. Use **Progressive Disclosure** - don't tell Claude all the information you could possibly want it to know. Rather, tell it _how to find_ important information so that it can find and use it, but only when it needs to to avoid bloating your context window or instruction count.
5. Claude is not a linter. Use linters and code formatters, and use other features like [Hooks](https://code.claude.com/docs/en/hooks) and [Slash Commands](https://code.claude.com/docs/en/slash-commands) as necessary.
6. **`CLAUDE.md` is the highest leverage point of the harness**, so avoid auto-generating it. You should carefully craft its contents for best results.


https://www.builder.io/blog/claude-md-guide

## How to structure your`CLAUDE.md`file

This is the meat of it. What actually belongs in the file?

### The essentials

**Project context**: What is this project? A one-liner that orients Claude. "This is a Next.js e-commerce app with Stripe integration" tells Claude more than you might think.

**Code style**: Your formatting and pattern preferences. Use ES modules or CommonJS? Prefer named exports? Be specific. "Format code properly" is vague.

**Commands**: How to run tests, build, lint, deploy. Claude will use these exact commands when you ask it to run things.

**Gotchas**: Project-specific warnings. That authentication module with the weird retry logic. The API endpoint that requires a specific header format. The file that should never be modified directly.

### A complete example

Here's what a `CLAUDE.md` might look like for a Next.js project:

```markdown
# Project: ShopFront

Next.js 14 e-commerce application with App Router, Stripe payments, and Prisma ORM.

## Code Style

- TypeScript strict mode, no `any` types
- Use named exports, not default exports
- CSS: Tailwind utility classes, no custom CSS files

## Commands

- `npm run dev`: Start development server (port 3000)
- `npm run test`: Run Jest tests
- `npm run test:e2e`: Run Playwright end-to-end tests
- `npm run lint`: ESLint check
- `npm run db:migrate`: Run Prisma migrations

## Architecture

- `/app`: Next.js App Router pages and layouts
- `/components/ui`: Reusable UI components
- `/lib`: Utilities and shared logic
- `/prisma`: Database schema and migrations
- `/app/api`: API routes

## Important Notes

- NEVER commit .env files
- The Stripe webhook handler in /app/api/webhooks/stripe must validate signatures
- Product images are stored in Cloudinary, not locally
- See @docs/authentication.md for auth flow details
```

Claude processes this efficiently because it's organized with clear headings, bullet points for scannability, and specific commands rather than vague instructions.

