# 🐧 Linux Software Processes

---

# 📚 Prerequisites

Before reading this chapter, you should understand:

- Why Docker
- Compute Device Components
- What is a Server?
- Scaling Servers
- Data Centers
- Introduction to Virtualization
- Hypervisors
- Virtual Machines
- Problems with Virtual Machines

---

# 📖 Definition

A **Process** is a **running instance of a program**.

When you execute a program, the operating system loads it into memory, assigns it system resources, and starts executing it. This running program is called a **Process**.

The Linux Kernel is responsible for creating, managing, and terminating processes.

> **Interview Definition**
>
> A Process is a running instance of a program that has its own Process ID (PID), memory, CPU time, and system resources managed by the operating system.

---

# 📜 Why Are We Learning About Processes?

You might be wondering...

> "I'm learning Docker. Why am I studying Processes?"

Because a **Container is simply an isolated Linux Process.**

If you don't understand what a process is, understanding containers becomes much harder.

This chapter builds the foundation for the next chapter: **Containers**.

---

# 📂 Program vs Process

Many beginners confuse these two terms.

They are **not the same thing.**

## Program

A **Program** is simply a file stored on disk.

Example:

```text
calculator.py

or

chrome.exe

or

ping
```

A program is **not running**.

It is just instructions written by a developer.

---

## Process

A **Process** is a program that is currently executing.

For example,

when you run:

```bash
python calculator.py
```

Linux creates a Process.

So,

```
Program + Execution = Process
```

---

# 🧠 English Explanation

Suppose you wrote a simple Python calculator.

```
calculator.py
```

This file is only stored on your computer.

Nothing is happening.

The moment you execute:

```bash
python calculator.py
```

Linux performs several operations:

1. Loads the program into memory.
2. Creates a Process.
3. Assigns a unique Process ID (PID).
4. Allocates CPU time.
5. Allocates memory.
6. Starts executing the code.

Now the program becomes a **Process**.

When execution finishes,

the Process is destroyed.

---

# 💡 Hinglish Explanation

Maan lo tumne ek Python calculator banaya.

```
calculator.py
```

Abhi ye sirf ek file hai.

Kuch bhi run nahi ho raha.

Jaise hi tum command chalate ho:

```bash
python calculator.py
```

Linux Kernel kaam shuru karta hai.

Ye:

- Program ko RAM mein load karta hai.
- Ek Process banata hai.
- PID assign karta hai.
- CPU time deta hai.
- Memory allocate karta hai.
- Program execute karna shuru karta hai.

Ab ye sirf file nahi rahi.

Ye ek **Running Process** ban gayi.

Program complete hote hi process terminate ho jaata hai.

---

# 🔄 Process Lifecycle

```
Program

↓

Execute

↓

Linux Kernel

↓

Create Process

↓

Running

↓

Completed

↓

Process Ends
```

---

# ⚙️ What Does Linux Kernel Do?

Whenever you run a program,

the Linux Kernel performs several tasks.

---

## 1️⃣ Loads Program into Memory

The program is copied from storage (SSD/HDD) into RAM.

Without RAM,

the CPU cannot execute it.

---

## 2️⃣ Assigns a Process ID (PID)

Every Process gets a unique Process ID.

Example:

```
PID = 2056

PID = 3010

PID = 4981
```

The operating system uses the PID to identify and manage processes.

---

## 3️⃣ Allocates CPU Time

A Process **does not get its own CPU**.

Instead,

the Kernel schedules CPU time.

Example:

```
Chrome

↓

CPU Time

----------------

VS Code

↓

CPU Time

----------------

Python

↓

CPU Time
```

The CPU rapidly switches between processes.

This is called **CPU Scheduling**.

---

## 4️⃣ Allocates Memory

Every Process receives memory.

Memory is used to store:

- Variables
- Objects
- Program Instructions
- Temporary Data

Each process has its own memory space.

---

## 5️⃣ Provides System Resources

Processes may use:

- Files
- Network Connections
- Printers
- USB Devices

The Kernel manages access to all these resources.

---

# 🏗️ Process Architecture

```
               Program

                  │

                  ▼

        Linux Kernel

                  │

      ┌───────────┼───────────┐

      ▼           ▼           ▼

   Memory       CPU Time     PID

                  │

                  ▼

           Running Process
```

---

# 🌍 Real-Life Analogy

Imagine a recipe book.

The recipe itself does nothing.

It is just instructions.

When a chef starts cooking,

the recipe becomes an actual meal.

Similarly,

```
Recipe

↓

Chef Cooking

↓

Finished Food
```

is similar to

```
Program

↓

Process

↓

Completed
```

A Program is like a recipe.

A Process is like someone actually cooking.

---

# 💻 Practical Example

Suppose you execute:

```bash
ping google.com
```

Linux Kernel will:

- Create a Process.
- Assign a PID.
- Allocate CPU time.
- Allocate Memory.
- Send ICMP packets.
- Display replies.

When you stop the command,

the Process ends.

---

# 📦 Why Is This Important for Docker?

Docker does **not** create Virtual Machines.

Docker creates **Containers**.

A Container is simply an **isolated Linux Process**.

That means when Docker starts a container,

the Linux Kernel creates a Process.

The difference is that Docker isolates that Process using Linux features such as:

- Namespaces
- Cgroups

We'll study these in later chapters.

---

# 🎤 Interview Answer

A Process is a running instance of a program. When a program is executed, the Linux Kernel loads it into memory, assigns it a Process ID (PID), allocates CPU time and memory, and manages its execution. Containers are built on this concept because every container is essentially an isolated Linux process.

---

# ⭐ Key Points

- A Program is a file.
- A Process is a running Program.
- Linux Kernel manages Processes.
- Every Process has a unique PID.
- Every Process receives Memory.
- Every Process receives CPU scheduling time.
- Containers are isolated Linux Processes.

---

# ❌ Common Mistakes

### ❌ Program and Process are the same.

✅ Wrong.

A Program is stored on disk.

A Process is the running version of that Program.

---

### ❌ Every Process gets its own CPU.

✅ Wrong.

Processes share the CPU.

The Kernel schedules CPU time.

---

### ❌ A Process runs forever.

✅ Wrong.

Processes terminate after execution unless they are long-running services.

---

### ❌ Docker creates Virtual Machines.

✅ Wrong.

Docker creates isolated Linux Processes.

---

# 🧠 Interview Deep Dive

## Why does every Process have a PID?

Because the operating system must uniquely identify every running Process.

Without PIDs,

the operating system would not know which process to:

- Pause
- Resume
- Stop
- Monitor

---

## Can multiple Processes run at the same time?

Yes.

Modern operating systems rapidly switch CPU time between processes.

On multi-core CPUs,

many processes can also execute simultaneously.

---

## Why is Process Isolation Important?

Isolation prevents one process from directly interfering with another process.

This improves:

- Stability
- Security
- Reliability

Docker extends this idea further by creating isolated container processes.

---

# ❓ Frequently Asked Interview Questions

### Q1. What is a Process?

A Process is a running instance of a program.

---

### Q2. What is the difference between a Program and a Process?

A Program is stored on disk.

A Process is a Program currently executing.

---

### Q3. What is a PID?

PID stands for **Process ID**, a unique identifier assigned to every running process.

---

### Q4. Who manages Processes in Linux?

The Linux Kernel.

---

### Q5. Why are Processes important in Docker?

Because every Docker Container is essentially an isolated Linux Process.

---

# 🧩 Connection to Docker

Now we understand that every running application is actually a Process.

Docker takes this concept one step further.

Instead of creating a complete Virtual Machine,

Docker simply creates an **isolated Process** that contains:

- Application Code
- Runtime
- Libraries
- Dependencies
- Environment Variables
- Configuration Files

This makes Containers much lighter and faster than Virtual Machines.

In the next chapter, we'll learn exactly **what a Container is** and why it became one of the biggest innovations in modern software development.

---

# 📝 Summary

A Process is a running instance of a program managed by the Linux Kernel. When a program is executed, the kernel loads it into memory, assigns it a unique Process ID (PID), allocates CPU time and memory, and starts execution. Understanding processes is essential because Docker containers are fundamentally isolated Linux processes rather than separate virtual machines.