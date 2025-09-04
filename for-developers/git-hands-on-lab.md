# Git Hands-On Lab
## Complete Guide to Git CLI Operations

This comprehensive hands-on lab will walk you through all essential Git operations using the command line interface. You'll learn by doing, covering everything from basic operations to advanced conflict resolution.

### Prerequisites
- Git installed on your system
- A GitHub account (or access to any Git remote repository service)
- Terminal/Command Line access

### Lab Overview
This lab covers:
1. **Repository Setup & Cloning**
2. **Basic Git Operations** (add, commit, push)
3. **Branching & Branch Management**
4. **Making Changes on Branches**
5. **Merging Branches**
6. **Creating & Resolving Conflicts**
7. **Commit History Management** (revert)
8. **Tagging & Tag Management**
9. **Cleanup & Best Practices**

---

## Lab Setup

### Step 1: Create a Practice Repository on GitHub
1. Go to GitHub and create a new repository called `git-lab-practice`
2. Initialize it with a README.md file
3. Copy the repository URL (it will look like: `https://github.com/yourusername/git-lab-practice.git`)

### Step 2: Set Up Your Local Environment
```bash
# Navigate to your working directory
cd ~/tmp

# Set your Git configuration (if not already done)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

---

## Section 1: Cloning and Initial Setup

### Clone the Repository
```bash
# Clone your repository
git clone https://github.com/UriBer/git-labs.git

# Navigate into the cloned repository
cd git-labs

# Check the current status
git status

# View the repository structure
ls -la

# Check remote configuration
git remote -v
```

**Expected Output**: You should see your repository files and the remote origin pointing to your GitHub repository.

---

## Section 2: Basic Git Operations

### Making Your First Commit

```bash
# Create a new file
echo "# Git Lab Practice Project" > project-info.md
echo "This repository is for practicing Git operations." >> project-info.md

# Check status to see untracked files
git status

# Add the file to staging area
git add project-info.md

# Check status again to see staged changes
git status

# Commit the changes
git commit -m "Add project information file"

# View commit history
git log --oneline

# Push changes to remote repository
git push origin main
```

### Adding More Content
```bash
# Create a source code file
cat << 'EOF' > app.py
#!/usr/bin/env python3

def greet(name):
    """A simple greeting function"""
    return f"Hello, {name}!"

def main():
    print(greet("Git Lab User"))

if __name__ == "__main__":
    main()
EOF

# Add and commit the new file
git add app.py
git commit -m "Add initial Python application"

# Create a configuration file
cat << 'EOF' > config.json
{
    "app_name": "Git Lab Practice",
    "version": "1.0.0",
    "author": "Lab Participant",
    "settings": {
        "debug": true,
        "max_users": 100
    }
}
EOF

# Add and commit configuration
git add config.json
git commit -m "Add application configuration"

# Push all changes
git push origin main

# View the commit history
git log --oneline --graph
```

---

## Section 3: Creating and Working with Branches

### Create a New Branch
```bash
# Create and switch to a new branch called 'feature/user-input'
git checkout -b feature/user-input

# Verify you're on the new branch
git branch

# Alternative way to create and switch to branch
# git switch -c feature/user-input  # Modern Git command
```

### Make Changes on the Branch
```bash
# Modify the Python application to accept user input
cat << 'EOF' > app.py
#!/usr/bin/env python3
import json

def load_config():
    """Load configuration from config.json"""
    with open('config.json', 'r') as f:
        return json.load(f)

def greet(name):
    """A simple greeting function"""
    return f"Hello, {name}!"

def main():
    config = load_config()
    print(f"Welcome to {config['app_name']} v{config['version']}")
    
    # Get user input
    user_name = input("Please enter your name: ")
    print(greet(user_name))
    
    print(f"Debug mode: {config['settings']['debug']}")

if __name__ == "__main__":
    main()
EOF

# Check what changed
git diff

# Stage and commit changes
git add app.py
git commit -m "Add user input functionality and config loading"

# Push the new branch to remote
git push -u origin feature/user-input
```

---

## Section 4: Creating Another Branch from Current Branch

### Create a Branch from Feature Branch
```bash
# Create another branch from the current feature branch
git checkout -b feature/enhanced-output

# Add enhanced output functionality
cat << 'EOF' > app.py
#!/usr/bin/env python3
import json
from datetime import datetime

def load_config():
    """Load configuration from config.json"""
    with open('config.json', 'r') as f:
        return json.load(f)

def greet(name):
    """A simple greeting function with timestamp"""
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    return f"Hello, {name}! (Greeted at {timestamp})"

def main():
    config = load_config()
    print(f"Welcome to {config['app_name']} v{config['version']}")
    print("-" * 40)
    
    # Get user input
    user_name = input("Please enter your name: ")
    greeting = greet(user_name)
    print(greeting)
    
    print("-" * 40)
    print(f"Debug mode: {config['settings']['debug']}")
    print(f"Max users supported: {config['settings']['max_users']}")

if __name__ == "__main__":
    main()
EOF

# Create a requirements file
echo "# No external dependencies required for this simple app" > requirements.txt

# Commit the enhanced version
git add app.py requirements.txt
git commit -m "Add enhanced output with timestamps and requirements file"

# Push the enhanced branch
git push -u origin feature/enhanced-output
```

---

## Section 5: Merging Branches

### Merge Feature Branch to Main
```bash
# Switch back to main branch
git checkout main

# Make sure main is up to date
git pull origin main

# Merge the feature branch
git merge feature/user-input

# Check the result
git log --oneline --graph

# Push the merged changes
git push origin main
```

---

## Section 6: Creating and Resolving Conflicts

### Set Up for Conflicts
```bash
# Switch to main branch and make a conflicting change
git checkout main

# Modify the app.py file in a different way
cat << 'EOF' > app.py
#!/usr/bin/env python3
import json

def load_config():
    """Load configuration from config.json"""
    with open('config.json', 'r') as f:
        return json.load(f)

def greet(name):
    """A simple greeting function"""
    return f"Greetings, {name}! Welcome to our application."

def main():
    config = load_config()
    print(f"=== {config['app_name']} v{config['version']} ===")
    
    # Get user input
    user_name = input("What's your name? ")
    print(greet(user_name))
    
    if config['settings']['debug']:
        print("[DEBUG] Application running in debug mode")

if __name__ == "__main__":
    main()
EOF

# Commit this change
git add app.py
git commit -m "Update app with different greeting style and debug output"
```

### Create the Conflict
```bash
# Try to merge the enhanced-output branch (this will create conflicts)
git merge feature/enhanced-output

# Git will show conflict message - check the status
git status

# View the conflicted file
cat app.py
```

### Resolve the Conflict
```bash
# Open the file and manually resolve conflicts
# The file will contain conflict markers like:
# <<<<<<< HEAD
# (main branch changes)
# =======
# (feature branch changes)
# >>>>>>> feature/enhanced-output

# Let's create a resolved version that combines both features
cat << 'EOF' > app.py
#!/usr/bin/env python3
import json
from datetime import datetime

def load_config():
    """Load configuration from config.json"""
    with open('config.json', 'r') as f:
        return json.load(f)

def greet(name):
    """A simple greeting function with timestamp"""
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    return f"Greetings, {name}! Welcome to our application. (Greeted at {timestamp})"

def main():
    config = load_config()
    print(f"=== {config['app_name']} v{config['version']} ===")
    print("-" * 40)
    
    # Get user input
    user_name = input("What's your name? ")
    greeting = greet(user_name)
    print(greeting)
    
    print("-" * 40)
    if config['settings']['debug']:
        print("[DEBUG] Application running in debug mode")
    print(f"Max users supported: {config['settings']['max_users']}")

if __name__ == "__main__":
    main()
EOF

# Mark conflicts as resolved and commit
git add app.py
git add requirements.txt  # This was also part of the merge

# Complete the merge
git commit -m "Resolve merge conflicts between main and enhanced-output branches"

# Check the result
git log --oneline --graph

# Push the resolved merge
git push origin main
```

---

## Section 7: Commit History Management

### View Commit History
```bash
# View detailed commit history
git log --oneline --graph --all

# View commits with more details
git log --graph --pretty=format:'%h -%d %s (%cr) <%an>' --abbrev-commit

# Find a specific commit to revert (note the commit hash)
git log --oneline | head -5
```

### Revert a Commit
```bash
# Let's create a commit that we'll want to revert
echo "This is a temporary feature that we'll remove" > temp-feature.txt
git add temp-feature.txt
git commit -m "Add temporary feature (will be reverted)"

# Push the commit
git push origin main

# Now revert this commit (use the actual commit hash from your output)
# Replace 'COMMIT_HASH' with the actual hash from git log
TEMP_COMMIT=$(git log --oneline -n 1 | cut -d' ' -f1)
git revert $TEMP_COMMIT

# This creates a new commit that undoes the changes
git log --oneline -n 3

# Push the revert
git push origin main
```

### Reset vs Revert (Demonstration)
```bash
# Show the difference between reset and revert
echo "Understanding Git reset vs revert" > git-concepts.md
git add git-concepts.md
git commit -m "Add git concepts documentation"

# Show current log
echo "Current commit history:"
git log --oneline -n 5

# Soft reset (keeps changes staged)
echo "Performing soft reset to previous commit..."
git reset --soft HEAD~1
git status

# Re-commit
git commit -m "Re-add git concepts documentation after soft reset"

# Push changes
git push origin main
```

---

## Section 8: Tagging

### Create Lightweight Tags
```bash
# Create a lightweight tag for the current version
git tag v1.0.0

# List tags
git tag

# Create an annotated tag with message
git tag -a v1.0.1 -m "Release version 1.0.1 with user input and enhanced output"

# View tag information
git show v1.0.1
```

### Push Tags to Remote
```bash
# Push a specific tag
git push origin v1.0.0

# Push all tags
git push origin --tags

# Verify tags on remote
git ls-remote --tags origin
```

### Create Tags for Specific Commits
```bash
# View commit history
git log --oneline -n 5

# Tag a specific commit (replace COMMIT_HASH with actual hash)
FIRST_COMMIT=$(git log --oneline | tail -1 | cut -d' ' -f1)
git tag -a v0.1.0 $FIRST_COMMIT -m "Initial version with basic functionality"

# Push the new tag
git push origin v0.1.0

# List all tags with their commit info
git tag -l -n1
```

---

## Section 9: Advanced Git Operations

### Working with Remote Branches
```bash
# Fetch all remote branches
git fetch origin

# List all branches (local and remote)
git branch -a

# Create a local branch from remote branch
git checkout -b local-enhanced origin/feature/enhanced-output

# Delete remote branch (cleanup)
git push origin --delete feature/user-input
git push origin --delete feature/enhanced-output

# Delete local branches
git branch -d feature/user-input
git branch -d feature/enhanced-output
git branch -d local-enhanced
```

### Stashing Changes
```bash
# Make some temporary changes
echo "Work in progress..." >> app.py

# Stash the changes
git stash

# Check status (should be clean)
git status

# List stashes
git stash list

# Apply stashed changes
git stash pop

# Check status again
git status

# Discard the temporary changes
git checkout -- app.py
```

---

## Section 10: Repository Cleanup and Summary

### Clean Up Tags and Branches
```bash
# View all tags
git tag

# Delete a local tag
git tag -d v1.0.0

# Delete remote tag
git push origin --delete v1.0.0

# Final repository state
echo "=== Final Repository State ==="
echo "Branches:"
git branch -a
echo -e "\nTags:"
git tag
echo -e "\nRecent commits:"
git log --oneline -n 5
```

### Create a Summary Document
```bash
# Create a lab summary
cat << 'EOF' > lab-summary.md
# Git Hands-On Lab Summary

## What We Accomplished

### 1. Repository Management
- Cloned a repository from GitHub
- Configured Git user settings
- Pushed changes to remote repository

### 2. Basic Git Operations
- Created and edited files
- Used `git add` to stage changes
- Made commits with descriptive messages
- Pushed commits to remote repository

### 3. Branching
- Created branches with `git checkout -b`
- Switched between branches
- Created branches from other branches
- Pushed branches to remote

### 4. Merging
- Merged feature branches into main
- Handled fast-forward merges
- Resolved merge conflicts manually
- Completed merge commits

### 5. Conflict Resolution
- Created intentional conflicts
- Identified conflict markers
- Manually resolved conflicts
- Completed conflict resolution with merge commit

### 6. Commit Management
- Viewed commit history with `git log`
- Reverted commits with `git revert`
- Demonstrated difference between reset and revert

### 7. Tagging
- Created lightweight tags
- Created annotated tags with messages
- Tagged specific commits
- Pushed tags to remote repository
- Managed tag lifecycle

### 8. Advanced Operations
- Worked with remote branches
- Used git stash for temporary changes
- Cleaned up branches and tags

## Key Git Commands Learned

### Repository Operations
- `git clone <url>`
- `git remote -v`
- `git status`

### Basic Operations
- `git add <file>`
- `git commit -m "message"`
- `git push origin <branch>`
- `git pull origin <branch>`

### Branching
- `git checkout -b <branch-name>`
- `git branch`
- `git merge <branch-name>`

### History and Conflicts
- `git log --oneline --graph`
- `git revert <commit-hash>`
- `git reset --soft HEAD~1`

### Tagging
- `git tag <tag-name>`
- `git tag -a <tag-name> -m "message"`
- `git push origin --tags`

### Cleanup
- `git branch -d <branch-name>`
- `git push origin --delete <branch-name>`
- `git tag -d <tag-name>`

## Best Practices Learned
1. Always write descriptive commit messages
2. Use branches for feature development
3. Resolve conflicts carefully and test afterwards
4. Use annotated tags for releases
5. Keep commit history clean and meaningful
6. Push changes regularly to avoid conflicts
7. Use `git status` frequently to understand repository state

## Next Steps
- Practice with pull requests/merge requests
- Learn about Git hooks
- Explore advanced Git workflows (Git Flow, GitHub Flow)
- Study Git internals and object model
EOF

# Add and commit the summary
git add lab-summary.md
git commit -m "Add comprehensive lab summary and best practices"

# Final push
git push origin main

echo "=== Git Hands-On Lab Completed Successfully! ==="
echo "Check your GitHub repository to see all the changes."
echo "Summary document created: lab-summary.md"
```

---

## Verification Steps

After completing the lab, verify your learning by running these commands:

```bash
# Verify repository state
echo "Repository branches:"
git branch -a

echo -e "\nRepository tags:"
git tag

echo -e "\nRecent commit history:"
git log --oneline --graph -n 10

echo -e "\nRemote configuration:"
git remote -v

echo -e "\nRepository status:"
git status
```

---

## Troubleshooting Common Issues

### Authentication Issues
If you encounter authentication problems:
```bash
# For HTTPS (will prompt for credentials)
git remote set-url origin https://github.com/username/git-lab-practice.git

# For SSH (requires SSH key setup)
git remote set-url origin git@github.com:username/git-lab-practice.git
```

### Merge Conflict Help
If you get stuck with merge conflicts:
```bash
# Abort the merge and start over
git merge --abort

# Or get help with merge tools
git mergetool
```

### Branch Issues
If you're on the wrong branch:
```bash
# See all branches
git branch -a

# Switch to correct branch
git checkout main
```

---

**Congratulations!** You've completed a comprehensive Git hands-on lab covering all major Git CLI operations. You now have practical experience with:

- Repository cloning and setup
- Basic Git workflow (add, commit, push)
- Branch creation and management
- Merging and conflict resolution
- Commit history management
- Tagging and release management
- Repository cleanup and maintenance

Keep practicing these commands in your daily development work to become proficient with Git!
