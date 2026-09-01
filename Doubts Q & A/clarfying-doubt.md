#26-08-2026

1. Forward Proxy vs NAT Gateway
2. Reverse Proxy vs Load Balancer
3. Nginx as Reverse Proxy
4. AWS NAT Gateway vs Internet Gateway

01-09-2026

# Linux Shells — Learning Notes

**Date:** 01-09-2026  
**Topic:** Linux Shell, Bash, sh, ksh, csh, Xshell

---

## 1. What is a Shell?

A **shell** is a program that provides an interface between the user and the operating system.

It reads the commands entered by the user, interprets them, and executes the required programs.

### Basic flow

```text
User
 ↓
Terminal
 ↓
Shell (Bash)
 ↓
Linux commands/programs
 ↓
Linux Kernel
 ↓
Hardware
```

Example:

```bash
ls
```

Bash interprets the command and executes the `ls` program.

---

## 2. What is Bash?

**Bash = Bourne Again Shell**

Bash is one of the most commonly used shells on Linux.

It is an improved shell based on the older Bourne Shell (`sh`) and provides many additional features.

Bash supports:

- Variables
- Conditions
- Loops
- Functions
- Pipes
- Redirection
- Environment variables
- Command substitution
- Shell scripting
- Job/process control

Example:

```bash
#!/bin/bash

NAME="Varun"

echo "Hello $NAME"
```

Bash is very important for DevOps because it is commonly used for:

- Linux administration
- AWS automation
- CI/CD pipelines
- Deployment scripts
- Docker automation
- Kubernetes scripts
- Log processing
- Server administration
- Troubleshooting

---

## 3. What is `sh`?

`sh` stands for **Bourne Shell**.

It is one of the original Unix shells.

Bash was designed to be largely compatible with `sh` while adding more functionality.

Example:

```bash
#!/bin/sh
```

This tells the operating system to execute the script using the `sh` interpreter.

Important:

```bash
#!/bin/bash
```

and

```bash
#!/bin/sh
```

are not always identical.

On some Linux distributions, `/bin/sh` may point to another shell implementation such as `dash`.

---

## 4. What is Korn Shell (`ksh`)?

**Korn Shell = ksh**

Korn Shell was developed at Bell Labs and provides features for both interactive shell usage and scripting.

It is still encountered in some enterprise Unix environments and legacy systems.

Examples of environments where it may be encountered:

- AIX
- Solaris
- Legacy enterprise systems
- Some banking environments

For modern DevOps learning, Bash has a higher priority than ksh.

---

## 5. What is C Shell (`csh`)?

**C Shell = csh**

C Shell was designed with syntax influenced by the C programming language.

Example:

```csh
if ( -f file.txt ) then
    echo "File exists"
endif
```

This syntax is different from Bash.

C Shell is historically important but is generally lower priority for modern Linux/DevOps work.

---

## 6. What is Xshell?

**Xshell is NOT a shell.**

Xshell is a **terminal/SSH client** that can be used to connect to remote servers.

Example:

```text
Your Computer
     |
   Xshell
     |
    SSH
     |
Linux Server
     |
   Bash
     |
Linux Kernel
```

Xshell provides the interface and SSH connection.

Bash is the shell that interprets commands on the Linux server.

Other terminal/SSH clients can also connect to Linux servers.

---

## 7. Terminal vs Shell vs Kernel

These three should not be confused.

### Terminal

Provides an interface for interacting with the shell.

Examples:

- Windows Terminal
- GNOME Terminal
- PuTTY
- Xshell

### Shell

Interprets commands and starts programs.

Examples:

- Bash
- sh
- zsh
- ksh
- csh

### Linux Kernel

The core of the Linux operating system.

It manages:

- CPU
- Memory
- Processes
- Filesystems
- Devices
- Networking
- System resources

---

## 8. Why are there multiple shells?

Different shells were developed at different times to provide different features, syntax, and compatibility.

Examples:

```text
sh
├── bash
├── ksh
├── zsh
└── other shells

csh
└── tcsh
```

Different organizations and users had different requirements, which led to the development of multiple shells.

It is similar to having multiple programming languages such as Python, Java, Go, C++, and Rust.

---

## 9. Common Linux Shells

| Shell | Full Name | Priority for DevOps |
|---|---|---|
| `sh` | Bourne Shell | High |
| `bash` | Bourne Again Shell | Very High |
| `zsh` | Z Shell | Medium |
| `ksh` | Korn Shell | Low/Medium |
| `csh` | C Shell | Low |
| `tcsh` | TENEX C Shell | Low |
| `fish` | Friendly Interactive Shell | Low |

For DevOps/SRE:

```text
Bash
 ↓
Shell scripting
 ↓
Linux commands
 ↓
Automation
```

should be the main focus.

---

# Important DevOps Concepts

### Shell scripting

Shell scripts allow us to automate repetitive Linux tasks.

Example:

```bash
#!/bin/bash

for file in *.log
do
    echo "$file"
done
```

Instead of manually performing the same operation many times, we can automate it using a script.

### Shebang

The first line of a shell script can specify the interpreter:

```bash
#!/bin/bash
```

This is called a **shebang**.

It tells the system which interpreter should execute the script.

### Check current