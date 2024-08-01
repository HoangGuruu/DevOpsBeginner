![Alt texts](../Images/p1.png)

# DevOps Beginner | Day 106 | Work with Git | GitHub | GitHub Action

```sh

#!/bin/bash

# Install Git
sudo apt-get install git

# Configure Git user
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"

# Initialize a new Git repository
git init

# Clone a remote repository
git clone https://github.com/user/repository.git

# Check the status of the repository
git status

# Add a file to the staging area
git add filename
# Add all changes
git add .

# Commit changes with a message
git commit -m "Commit message"

# View the commit history
git log

# Push changes to the remote repository
git push origin branch-name

# Pull changes from the remote repository
git pull origin branch-name

# Create a new branch
git checkout -b new-branch-name

# Switch to another branch
git checkout branch-name

# Merge a branch into the current branch
git merge branch-name

# Delete a branch
git branch -d branch-name
# Delete a remote branch
git push origin --delete branch-name

# Show differences between versions
git diff

# Restore a file from the previous commit
git checkout -- filename

# Reset to a previous commit
git reset --hard commit-id

# Add a remote repository
git remote add origin https://github.com/user/repository.git

# View remote repositories
git remote -v

# Remove a file from git and the file system
git rm filename

# Move or rename a file
git mv old-filename new-filename

# Create a tag
git tag -a v1.0 -m "Version 1.0"
# Push the tag to the remote repository
git push origin v1.0

# Stash changes temporarily
git stash
# Restore stashed changes
git stash pop

# View stash details
git stash list

# Drop a stash
git stash drop

```