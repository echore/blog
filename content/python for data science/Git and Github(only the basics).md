---
share: true
---
The video:
https://youtu.be/4dkNn93DIx4?si=tcwcsMQ_l7oVeTld

I used AI to give me some tips and they are helpful:
Here are the most basic Git commands for beginners to connect VSCode with GitHub:

1. First-time setup (only need to do once):
```bash
# Set your identity
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

2. Start a new project:
```bash
# Initialize a new Git repository
git init

# Or clone an existing project
git clone https://github.com/username/repository.git
```

3. Basic daily commands:
```bash
# Check file status
git status

# Add files to staging area
git add .  # add all files
git add filename  # add specific file

# Commit changes
git commit -m "describe your changes"

# Push to GitHub
git push origin main  # or git push origin master
```

4. Update code:
```bash
# Pull latest code from GitHub
git pull origin main  # or git pull origin master
```

