# ⭐Week 4: Git and GitHub Challenge

## Tasks

### Task 1: Fork and Clone the Repository

 **1.Fork the Repository:**

Visit this repository and fork it to your own GitHub account. If not done yet.

 **2.Clone Your Fork Locally:**

 Clone the forked repository using HTTPS:

  git clone <your-fork-url>

Change directory into the cloned repository:

cd 2025/git/01_Git_and_Github_Basics

![alt text](<Screenshot (567).png>)

### Task 2: Initialize a Local Repository and Create a File

**1.set Up Your Challenge Directory:**

1.Inside the cloned repository, create a new directory for this challenge:
>> Commands

mkdir week-4-challenge

cd week-4-challenge

2.Initialize a Git Repository:
 
 command

 git init

 3.Create a File:

Create a file named info.txt and add some initial content (for example, your name and a brief introduction).

4.Stage and Commit Your File:

Stage the file:

command:git add info.txt

Commit the file with a descriptive message:

command:git commit -m "Initial commit: Add info.txt with introductory content"

![alt text](<Screenshot (570).png>)

## Task 3: Configure Remote URL with PAT and Push/Pull

1.Configure Remote URL with Your PAT:
To avoid entering your Personal Access Token (PAT) every time you push or pull, update your remote URL to include your credentials.

Replace <your-username>, <your-PAT>, and <repository-name> with your actual GitHub username, your PAT, and the repository name respectively:

command:git remote add origin https://<your-username>:<your-PAT>@github.com/<your-username>/90DaysOfDevOps.git

If a remote named origin already exists, update it with:

command:git remote set-url origin https://<your-username>:<your-PAT>@github.com/<your-username>/90DaysOfDevOps.git

2.Push Your Commit to Remote:

Push your current branch (typically main) and set the upstream:
git push -u origin main

![alt text](<Screenshot (569).png>)

## Task 4: Explore Your Commit History

1. View the Git Log:

command : git log

![alt text](<Screenshot (568).png>)

## Task 5: Advanced Branching and Switching

1. Create a New Branch:

  Create a branch called feature-update:

   command : git branch feature-update

2.Switch to the New Branch:

  Switch using git switch:

command : git switch feature-update

3.Modify the File and Commit Changes:

Edit info.txt 

Stage and commit your changes:

commands :

git add info.txt

git commit -m "Feature update: Enhance info.txt with additional details"

git push origin feature-update

![alt text](<Screenshot (572).png>)

Merge this branch to main via a Pull Request on GitHub.

![alt text](<Screenshot (573).png>)

![alt text](<Screenshot (574).png>)

## Task 6: Explain Branching Strategies

1. List all the Git commands you used in Tasks 1–4.

**Initialize repository**
git init

**Check repository status**
git status

**Add files to staging area**
git add .
git add <file_name>

**Commit changes**
git commit -m "Initial commit"

**View commit history**
git log
git log --oneline

**Create a new branch**
git branch feature-update

**Switch to a branch**
git switch feature-update
**or**
git checkout feature-update

**Make changes and commit**
git add info.txt
git commit -m "Updated info file in feature branch"

**Switch back to main/master branch**
git switch master
**or**
git checkout master

**Merge feature branch into master**
git merge feature-update

**Push changes to GitHub**
git push origin master
git push origin feature-update

## 🔹 Why Branching Strategies Are Important in Collaborative Development

Branching strategies play a crucial role in team-based software development. They help manage code efficiently and reduce risks during development.

1️⃣ **Isolating Features and Bug Fixes**

Branches allow developers to work on new features or bug fixes separately without affecting the stable main branch.
For example, creating a feature-update branch ensures that experimental or incomplete work does not break production-ready code.

2️⃣ **Facilitating Parallel Development**

Multiple developers can work simultaneously on different features using separate branches.
This improves productivity and prevents overwriting each other’s work.

3️⃣ **Reducing Merge Conflicts**

When changes are organized into specific branches (feature, bugfix, hotfix), conflicts are easier to manage.
Frequent merging and clear branching strategies reduce the chances of large, complex conflicts.

4️⃣ **Enabling Effective Code Reviews**

Branches make it easier to create Pull Requests on platforms like GitHub.
Team members can review code changes before merging them into the main branch, ensuring better code quality and fewer bugs.
