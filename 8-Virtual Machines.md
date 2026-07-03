# 💻 Virtual Machines (VMs)

---

# 📚 Prerequisites

Before reading this chapter, you should understand:

- Compute Device Components
- What is a Server?
- Scaling Servers
- Data Centers
- Introduction to Virtualization
- Hypervisors

---

# 📖 Definition

A **Virtual Machine (VM)** is a software-based computer that behaves like a physical computer.

Each Virtual Machine has its own:

- Operating System
- CPU (vCPU)
- RAM (vRAM)
- Storage (vDisk)
- Network Interface (vNIC)

Although multiple Virtual Machines share the same physical server, each VM operates independently as if it were its own computer.

---

# 📜 History

Before virtualization became popular, organizations typically ran **one application on one physical server**.

This approach caused:

- High hardware costs
- Low hardware utilization
- Difficult maintenance
- Poor scalability

Virtualization introduced the concept of Virtual Machines, allowing multiple isolated computers to run on a single physical server.

Today, Virtual Machines are widely used in:

- Data Centers
- Cloud Computing
- AWS
- Microsoft Azure
- Google Cloud Platform

---

# 🎯 Why Do We Need Virtual Machines?

Imagine a company has one powerful physical server.

```
CPU      : 64 Cores
RAM      : 256 GB
Storage  : 8 TB
```

The company has four different applications.

```
Application A → Python

Application B → Java

Application C → .NET

Application D → MySQL
```

If all applications run directly on one Operating System,

they may create:

- Dependency conflicts
- Runtime conflicts
- Security risks
- Difficult maintenance

Virtual Machines solve this problem by giving each application its own isolated environment.

---

# 🧠 English Explanation

A Virtual Machine is an independent software computer.

Although it runs on shared hardware,

it behaves exactly like a real computer.

Each VM has:

- Its own Operating System
- Its own file system
- Its own memory allocation
- Its own CPU allocation
- Its own network configuration

Applications running inside one VM cannot directly affect another VM.

This isolation makes Virtual Machines reliable and secure.

---

# 💡 Hinglish Explanation

Socho tumhare paas ek bahut powerful server hai.

Usme virtualization enable hai.

Hypervisor us server ko divide karta hai aur multiple Virtual Machines bana deta hai.

Har VM ko lagta hai ki woh ek alag computer hai.

Example:

VM 1

Ubuntu

Python Application

----------------------

VM 2

Windows Server

.NET Application

----------------------

VM 3

CentOS

MySQL Database

Ye teeno same physical server par chal rahe hain.

Lekin inhe pata bhi nahi hota ki ye hardware share kar rahe hain.

Har VM apne aap mein ek complete computer hoti hai.

---

# 🏗️ Architecture

```
                     Physical Server

+---------------------------------------------------------+
| CPU | RAM | Storage | Network                           |
+---------------------------------------------------------+
                     │
                     ▼
+---------------------------------------------------------+
|                     Hypervisor                          |
+---------------------------------------------------------+
          │                 │                 │
          ▼                 ▼                 ▼

+----------------+  +----------------+  +----------------+
|      VM 1      |  |      VM 2      |  |      VM 3      |
|----------------|  |----------------|  |----------------|
| Ubuntu         |  | Windows        |  | CentOS         |
| Python App     |  | .NET App       |  | MySQL          |
+----------------+  +----------------+  +----------------+
```

Each VM is completely isolated.

---

# ⚙️ Components of a Virtual Machine

Every Virtual Machine receives virtual hardware from the Hypervisor.

---

## vCPU

The Hypervisor allocates virtual CPU cores.

Example:

```
Physical CPU

↓

64 Cores

↓

VM1 → 8 vCPU

VM2 → 16 vCPU

VM3 → 4 vCPU
```

---

## vRAM

The Hypervisor allocates virtual memory.

Example:

```
Physical RAM

↓

256 GB

↓

VM1 → 32 GB

VM2 → 64 GB

VM3 → 16 GB
```

---

## vDisk

Each VM receives virtual storage.

Example:

```
Physical SSD

↓

8 TB

↓

VM1 → 500 GB

VM2 → 1 TB

VM3 → 300 GB
```

---

## vNIC

Each VM gets its own virtual network adapter.

This allows every VM to communicate independently over the network.

---

# 🌍 Real-Life Analogy

Imagine a hotel.

The hotel building represents the Physical Server.

Each room represents a Virtual Machine.

Every guest gets:

- Their own room
- Their own bed
- Their own bathroom
- Their own key

Although everyone shares the same building,

each guest has a separate private space.

Virtual Machines work exactly the same way.

---

# 💻 Practical Example

Suppose a company develops three applications.

Application 1

Python 3.12

Ubuntu

----------------------

Application 2

Java 21

Windows Server

----------------------

Application 3

PostgreSQL

CentOS

Instead of buying three physical servers,

the company creates three Virtual Machines.

Each VM runs independently while sharing the same physical hardware.

---

# 🎤 Interview Answer

A Virtual Machine is a software-based computer that runs on a physical server using a Hypervisor. Each Virtual Machine has its own operating system, virtual hardware, and isolated environment, allowing multiple operating systems and applications to run safely on the same physical machine.

---

# ⭐ Advantages of Virtual Machines

- Better hardware utilization
- Strong isolation
- Supports multiple Operating Systems
- Easy migration
- Better security
- Easier testing
- Disaster recovery
- Snapshots and backups

---

# ❌ Disadvantages of Virtual Machines

Although Virtual Machines solve many problems,

they introduce new challenges.

Every Virtual Machine requires:

- A complete Operating System
- System libraries
- Boot process
- Kernel
- Storage space

As a result:

- High memory usage
- Large storage requirements
- Slower startup
- Higher resource consumption

These problems eventually led to Containers.

---

# ⭐ Key Points

- A VM behaves like a real computer.
- Every VM has its own Operating System.
- Virtual hardware is provided by the Hypervisor.
- Multiple VMs share one physical server.
- VMs are isolated from one another.

---

# ❌ Common Mistakes

### ❌ A VM is just an application.

✅ Wrong.

A VM is a complete virtual computer.

---

### ❌ Virtual Machines share the same Operating System.

✅ Wrong.

Every VM has its own Guest Operating System.

---

### ❌ A VM directly controls the hardware.

✅ Wrong.

The Hypervisor controls the physical hardware.

---

# 🧠 Interview Deep Dive

## Why does every VM need its own Operating System?

Because every Virtual Machine behaves like an independent computer.

It must boot independently,

manage its own memory,

run its own processes,

and maintain its own kernel.

---

## Why are Virtual Machines considered heavyweight?

Because every VM contains:

- Guest Operating System
- Kernel
- Libraries
- Drivers
- Bootloader

Even if your application is only 200 MB,

the VM may consume several gigabytes of storage.

---

# ❓ Frequently Asked Interview Questions

### Q1. What is a Virtual Machine?

A software-based computer that runs on shared physical hardware using a Hypervisor.

---

### Q2. Can multiple Operating Systems run on one server?

Yes.

Each Virtual Machine can run a different Operating System.

---

### Q3. Why are Virtual Machines isolated?

Because the Hypervisor allocates separate virtual hardware and resources to each VM.

---

### Q4. Why are Virtual Machines called heavyweight?

Because every VM contains its own complete Operating System and related system files.

---

### Q5. What is the difference between a Physical Server and a Virtual Machine?

A Physical Server is real hardware.

A Virtual Machine is a software-based computer running on that hardware.

---

# 🧩 Connection to Docker

Virtual Machines solved many problems such as hardware utilization and application isolation.

However, every VM still required a complete Operating System.

Imagine creating 100 Virtual Machines.

You now have 100 Operating Systems running simultaneously.

This leads to:

- High RAM usage
- Large storage consumption
- Slow boot times
- Higher maintenance overhead

Engineers started asking a new question:

> **"Can we isolate applications without running a complete Operating System every time?"**

That question gave birth to **Containers**.

---

# 📝 Summary

Virtual Machines allow multiple independent computers to run on a single physical server.

Each VM has its own Operating System, virtual hardware, and isolated environment, making them ideal for running different applications safely.

Although VMs significantly improved hardware utilization and flexibility, their dependence on separate operating systems introduced performance and resource overhead, paving the way for container technology.