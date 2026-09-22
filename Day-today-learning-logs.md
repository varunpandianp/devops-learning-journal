**📅 26-08-2026**

🧠 What I Learned

GitHub basics — repositories, commits, commit messages and basic GitHub workflow

Refactored and reorganized my DevOps learning repositories

Networking fundamentals

OSI Model — 7 layers, responsibilities and protocols

IP Address — IPv4, Public IP and Private IP

IP Classes — Class A, B, C, D and E

Forward Proxy and Reverse Proxy

NAT Gateway and NAT concepts

VPN and encrypted tunneling

Load Balancer — basic concept and use case

🔑 Quick Revision

OSI → MAC → IP → Port → Protocol

Forward Proxy → Client

Reverse Proxy → Server

NAT → Private network → Internet

VPN → Secure tunnel

Load Balancer → Distributes traffic

**📅 27-08-2026 — Learning Progress**

🧠 Learning Activities
- Learned IP address fundamentals — IPv4, Public IP, Private IP and IP classes.
- - Understood encapsulation — Data → Segment → Packet → Frame → Bits.
- Understood TCP/IP in modern networks and how it relates to the OSI model.
- Clarified the role of the Session Layer and how session management is handled in modern applications.
- Learned DNS fundamentals — domain name resolution, DNS hierarchy, recursive resolver, authoritative DNS and how a domain is resolved to an IP address.

🔑 Quick Revision
L7–L5 → Data | L4 → Segment/TCP/UDP | L3 → Packet/IP | L2 → Frame/MAC | L1 → Bits

Client - | DNS - recursive resolver | - root - | TLD .com | - authoritative DNS |- IP

Learning Log — 28-08-2026

Topics Covered

Operating System (OS) Basics

Linux File System

Linux Directories

Basic Linux Commands 

31-08-2026
📅 31-08-2026 — Learning Progress
🧠 What I Learned
- Learned the DevOps lifecycle and CI/CD pipeline and how code moves from development to production.
- Understood CI vs CD and how CI/CD bridges Development and Operations through automation.
- Learned the role of Git, Jenkins, GitHub Actions, Maven, Docker, Terraform, Ansible, Kubernetes and Cloud in the DevOps pipeline.
- Understood the importance of testing, security, deployment, monitoring and feedback, and that DevOps is broader than just CI/CD.

## 📅 01-09-2026 — Learning Progress

### 🧠 What I Learned

- Learned **Linux fundamentals** — Linux architecture, kernel, shell, distributions and filesystem hierarchy.
- Practised **essential Linux commands** for navigation, file management, searching, reading logs, processes, resources and services.
- Learned **Linux pipes, redirection and command-line workflow**, including `grep`, `find`, `tail -f` and command composition.
- Learned basic **Linux troubleshooting** using `systemctl`, `journalctl`, `df`, `free`, `top` and understood their importance in DevOps/SRE environments.

## 📅 02-09-2026 — Learning Progress

### 🧠 What I Learned

- Learned **Linux users, groups, sudo and user management**, including UID, GID and important account files such as `/etc/passwd`, `/etc/group` and `/etc/sudoers`.
- Learned **Linux file permissions and ownership** — read/write/execute, `chmod`, numeric permissions, `chown`, `chgrp`, `umask` and special permissions.
- Learned **SSH and key-based authentication**, including SSH keys, `authorized_keys`, `scp`, `rsync`, SSH hardening and troubleshooting.
- Learned the fundamentals of the **vi/vim editor** and essential commands for editing files directly on Linux servers.

## 📅 03-09-2026 — Learning Progress

### 🧠 What I Learned

- Learned **Shell Scripting fundamentals** — shebang, variables, command substitution, quoting and script arguments.
- Learned **conditionals, loops and functions** to make Linux commands reusable and automate repetitive tasks.
- Learned **exit codes and error handling**, including `$?`, `exit 0`, non-zero exit codes, `set -euo pipefail` and stdout/stderr.
- Learned **shell scripting best practices** — validate inputs, quote variables, avoid hardcoded credentials, handle destructive commands carefully and use ShellCheck.

## Learning Log — 04-09-2026
- Learned Git & GitHub basics.
- Understood Git workflow: Working → Staging → Commit → Remote.
- Practiced git init, status, add, commit, diff, and log.
- Learned repositories, commits, and .gitignore.
- Understood Git ≠ GitHub.

## Learning Log — Git & GitHub Session 2

Date: 17-09-2026 session data :09-09-2026
- Learned Git undo commands: restore, revert, reset, stash.
- Learned Git branching and branch management.
- Learned merge and merge conflicts.
- Learned rebase, squash, and reflog.
- Practiced handling and recovering Git changes
- 
## Learning Log — Git & GitHub 
- Date: 18-09-2026 session data :10-09-2026
- Learned git reset: soft, mixed and hard.
- Understood reset vs revert and rebase.
- Learned git show and GitHub branch protection rules.
- Learned webhooks and GitHub Actions for CI/CD.
- Understood GitHub/GitLab workflow basics.

##  Learning Log  - build tools and build process 18-09-2026

- Learned about Build Tools.
- Learned Ant vs Maven vs Gradle.
- Understood Imperative vs Declarative build systems.
- Learned Maven project structure and `pom.xml`.
- Learned Maven dependency management and Maven Central.
- Learned Local Maven Repository (`~/.m2/repository`).
- Learned about Maven `settings.xml`.
- Learned the 3 Maven lifecycles: Clean, Default and Site.
- Practiced Maven build phases and basic Maven commands.

## Learning Log - CI/CD - Jenkins

**Session Date:** 14-09-2026  
**Study Date:** 21-09-2026

### Topics Covered

- Learned the basics of CI/CD.
- Understood Continuous Integration (CI) and Continuous Delivery/Deployment (CD).
- Learned what Jenkins is and how it is used for CI/CD automation.
- Understood Jenkins Controller and Jenkins Agent.
- Learned about Jenkins Jobs and Pipelines.
- Learned the purpose of a Jenkinsfile and Pipeline as Code.
- Understood Jenkins triggers and GitHub Webhooks.
- Learned Jenkins integration with Maven, Docker, Kubernetes, and AWS.
- Learned about Jenkins Credentials and secure handling of secrets.
- Understood the basic CI/CD flow from GitHub → Jenkins → Build → Test → Package → Deploy.

### Progress

Learned the fundamentals of Jenkins and understood how Jenkins fits into a real-world CI/CD pipeline.

## Learning Log - Jenkins Controller & Agent

**Session Date:** 14-09-2026  
**Study Date:** 21-09-2026

### Topics Covered

- Learned Jenkins Controller and Agent architecture.
- Understood the difference between Controller and Agent.
- Learned that Agents execute build, test, and deployment tasks.
- Understood that an Agent can be a separate EC2 instance, VM, physical server, container, or Kubernetes pod.
- Learned how the Controller assigns workloads to Agents.
- Understood the use of multiple Agents for distributing CI/CD workloads.
- Learned about Agent labels and different Agent capabilities.
- Understood static and dynamic Jenkins Agents.
- Learned the AWS example of using separate EC2 instances as Jenkins Agents.

### Progress

Understood how Jenkins Controller manages and distributes CI/CD workloads to Jenkins Agents.

## Learning Log - Jenkins Pipeline as Code

**Session Date:** 14-09-2026  
**Study Date:** 22-09-2026

### Topics Covered

- Learned Pipeline as Code in Jenkins.
- Understood the purpose of the Jenkinsfile.
- Learned how Jenkinsfile is stored and managed in Git.
- Understood the difference between Freestyle Jobs and Pipeline as Code.
- Learned Build as Code and the role of `pom.xml` in Maven.
- Understood how Jenkinsfile defines the CI/CD workflow.
- Learned the benefits of version-controlled pipeline configuration.

### Progress

Understood how Jenkins pipelines can be defined as code using a Jenkinsfile and managed through Git.