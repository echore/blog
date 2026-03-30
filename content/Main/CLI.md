---
share: true
---
2026-03-27  11:29
Tags:[[Technical Literacy|Technical Literacy]]


---

## 1. What is CLI?

**CLI = Command Line Interface**

> A way to interact with your computer by typing text commands instead of clicking buttons.

---

## 2. Intuition first (important)

### 🧠 Analogy

Think of your computer as a person:

- **GUI (Graphical UI)** → talking with gestures (clicking icons 🖱️)
    
- **CLI** → giving precise verbal instructions
    

Example:

- GUI: click folder → open file → click run
    
- CLI:
    

```bash
python script.py
```

👉 same goal, but CLI is:

- faster
    
- more precise
    
- scriptable
    

---

## 3. What does it actually look like?

On your computer, CLI is:

- Mac → **Terminal**
    
- Windows → **Command Prompt / PowerShell**
    

You’ll see something like:

```bash
XX@macbook ~ %
```

That’s your CLI waiting for commands.

---

## 4. Basic commands (you should know these)

Let’s build intuition step by step.

### 📁 Navigate folders

```bash
ls
```

→ list files (like opening a folder)

```bash
cd my_folder
```

→ go into a folder

```bash
cd ..
```

→ go back

---

### 📄 Work with files

```bash
touch file.txt
```

→ create file

```bash
rm file.txt
```

→ delete file

---

### ▶️ Run programs

```bash
python script.py
```

This is HUGE — this is how you:

- run ML scripts
    
- launch pipelines
    
- execute automation (like your n8n workflows later)
    

---

## 5. Why developers LOVE CLI

This is the real reason:

### (1) Speed

Typing > clicking

---

### (2) Automation (very important for you)

You can chain commands:

```bash
python preprocess.py && python train.py && python evaluate.py
```

👉 That’s basically a **mini pipeline**

---

### (3) Reproducibility

Instead of:

> “click this, then this, then this…”

You can say:

> “run this command”

---

### (4) Required for real tools

Things you want to learn:

- Git
    
- Docker
    
- APIs
    
- Cloud (AWS, GCP)
    

👉 all CLI-heavy

---
