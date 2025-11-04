# Week 10 – Version Control (Git & GitHub)

## 🎯 Task

- Creating repositories, cloning repositories, creating branches, committing and reverting commits, 
pulling and pushing changes downstream and upstream, fetching, merging and renaming branches, creating,
reviewing merging, reverting pull requests etc.

---
## 📖 Description
This week focused on applying version control best practices using **Git** and **GitHub**.  
The goal was to demonstrate practical skills in repository management, branching, committing, reviewing, merging, and reverting changes in a collaborative environment.

---

## 🏗️ Project Setup
- Repository Name: `backend-version-control-task-mohammad-bakur`
- Description:  
  A hands-on version control task showcasing my understanding of Git workflows using a Spring Boot project developed in previous weeks.

---

## 🌿 Branching Strategy
| Branch Name | Purpose |
|--------------|----------|
| `feature-user` | Added improvements and documentation for UserController and UserService tests |
| `feature-teacher` | Added repository test cases for TeacherRepository |
| `main` | Production-ready code after PR reviews and merges |

---

## 🧩 Commits
Each feature branch contains **at least three meaningful commits**, such as:
- Added Javadoc comments to UserService tests
- Improved naming conventions in TeacherRepositoryTest
- Updated README with version control notes

---

## 🔀 Pull Requests
- Created PRs from each feature branch to `main`.
- Added self-review comments and resolved discussions.
- Merged PRs after approval.

📸 *Screenshots of merged PRs and discussions were included in the repository.*

---

## 🔁 Reversion & Branch Renaming
- Simulated a mistake in one commit and reverted it using:
  ```bash
  git revert <commit-hash>

- Renamed a branch using:
  - git branch -m old-name new-name
  - git fetch origin

---
#### 🧰 Common Git Commands Used

- git init
- git clone
- git branch
- git checkout -b
- git add .
- git commit -m "Meaningful message"
- git push origin branch-name
- git pull origin main
- git merge branch-name
- git revert <commit-hash>
- git log --oneline

---


## 📚 🧠 🎓 Learning Outcome

Learned how to manage version control efficiently for a team project.

Understood branching workflows (feature branches and main).

Practiced writing meaningful commit messages.

Learned to handle PR reviews, merges, and reverts.

Strengthened collaboration habits for real-world projects.

---

## ✅ Summary

This module improved my collaboration and version control workflow understanding.
The Git-based approach ensures code integrity, traceability, and team efficiency.


