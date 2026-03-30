---
share: true
---
2026-03-29  21:49
Tags:[[Technical Literacy|Technical Literacy]]

## What is YAML?

**YAML** (short for _"YAML Ain't Markup Language"_) is a simple, human-readable format for writing structured data. It uses indentation and key-value pairs instead of complex syntax like HTML or JSON.

A basic example:

```yaml
name: John
age: 30
job: Designer
```

That's it — `key: value` pairs, plain and simple.

---

## What is "Frontmatter"?

Frontmatter is a **block of YAML placed at the very top of a file**, sandwiched between two sets of triple dashes (`---`). It's essentially metadata _about_ the file — information that describes the file itself rather than being the main content.

```
---
name: my-skill
description: This skill helps write emails
author: Jane
---

# The actual content of the file starts here...
```

Everything between the `---` lines is the frontmatter. Everything after is the real content.

---

## In the context of Claude Skills

When you create a SKILL.md file, the YAML frontmatter tells Claude the _who/what_ of the skill at a glance — without reading the whole file:

```yaml
---
name: email-writer
description: Helps draft professional emails in a concise tone
---
```

This matters because of how Claude loads Skills efficiently — it only scans the frontmatter first (name + description) to decide if a skill is relevant to your current task, then loads the full instructions only if needed. It's like a book cover before reading the whole chapter.

---

## Why triple dashes?

The `---` is just a widely adopted convention (originated from Markdown and static site generators like Jekyll) to signal "this section is metadata, not content." It's a separator that tools and AI can reliably detect.

---

**In short:** YAML frontmatter = a small labeled header at the top of a file that describes what the file is, written in a clean `key: value` format. Nothing more complicated than that!