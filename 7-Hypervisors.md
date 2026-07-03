# ⚙️ Hypervisors

---

# 📚 Prerequisites

Before reading this chapter, you should understand:

- Compute Device Components
- What is a Server?
- Scaling Servers
- Data Centers
- Introduction to Virtualization

---

# 📖 Definition

A **Hypervisor** (also called a **Virtual Machine Monitor (VMM)**) is a software layer that creates, runs, and manages **Virtual Machines (VMs)** on a physical computer.

It acts as a bridge between the physical hardware and the virtual machines, allowing multiple operating systems to share the same hardware safely and efficiently.

---

# 🎯 Why Do We Need a Hypervisor?

In the previous chapter, we learned that companies wanted to run multiple applications on the same physical server.

However, there was one problem.

A physical server has only one set of hardware resources:

- CPU
- RAM
- Storage
- Network Interface Card (NIC)

How can multiple operating systems use the same hardware at the same time?

The answer is **Hypervisor**.

A Hypervisor manages the physical resources and distributes them among multiple Virtual Machines.

Without a Hypervisor, virtualization would not be possible.

---

# 🧠 English Explanation

A Hypervisor is responsible for creating Virtual Machines.

Each Virtual Machine believes it owns the entire computer.

However, in reality, all Virtual Machines are sharing the same physical hardware.

The Hypervisor manages this sharing by allocating virtual resources such as:

- vCPU
- vRAM
- vDisk
- vNIC

to each Virtual Machine.

It also ensures that one VM cannot interfere with another VM.

This isolation is one of the biggest advantages of virtualization.

---

# 💡 Hinglish Explanation

Socho tumhare paas ek bahut powerful server hai.

Usme hai:

- 64 CPU Cores
- 256 GB RAM
- 8 TB SSD

Ab tum usme 10 Virtual Machines banana chahte ho.

Question ye hai...

Ye VMs hardware kaise share karengi?

CPU kaun use karega?

RAM kaise divide hogi?

Storage kaise milegi?

Ye saara kaam **Hypervisor** karta hai.

Hypervisor ek manager ki tarah kaam karta hai.

Ye decide karta hai ki kis VM ko kitna:

- CPU
- RAM
- Storage
- Network

milega.

Har VM ko lagta hai ki uske paas apna khud ka computer hai,

lekin actually sab ek hi physical server share kar rahe hote hain.

---

# 🏗️ Architecture

## Without Hypervisor

```
+-----------------------------------------+
|          Physical Hardware              |
|-----------------------------------------|
| CPU | RAM | Storage | Network           |
+-----------------------------------------+

Only one Operating System can run.
```

---

## With Hypervisor

```
+------------------------------------------------------+
|                   Virtual Machines                   |
|------------------------------------------------------|
| VM 1 | VM 2 | VM 3 | VM 4                            |
|------------------------------------------------------|
| Ubuntu | Windows | CentOS | Debian                   |
|------------------------------------------------------|
|              Hypervisor (VMM)                        |
|------------------------------------------------------|
| CPU | RAM | Storage | Network                        |
+------------------------------------------------------+
```

The Hypervisor sits between the hardware and the Virtual Machines.

---

# 🔧 Responsibilities of a Hypervisor

A Hypervisor performs several important tasks.

## 1️⃣ Creates Virtual Machines

It creates multiple Virtual Machines on a single physical server.

---

## 2️⃣ Allocates Hardware Resources

It distributes:

- Virtual CPU (vCPU)
- Virtual RAM (vRAM)
- Virtual Disk (vDisk)
- Virtual Network Interface (vNIC)

to each Virtual Machine.

---

## 3️⃣ Provides Isolation

Each Virtual Machine runs independently.

If one VM crashes,

the other VMs continue running.

---

## 4️⃣ Resource Management

The Hypervisor decides how physical resources are shared among Virtual Machines.

---

## 5️⃣ Hardware Abstraction

The Hypervisor hides the complexity of physical hardware.

Each VM simply sees virtual hardware.

---

# 🌍 Real-Life Analogy

Imagine a hotel.

The hotel building is the **Physical Server**.

Each room is a **Virtual Machine**.

Guests inside each room think they have their own private space.

The **Hotel Manager** decides:

- Which guest gets which room
- Who can enter
- Who gets electricity
- Who gets water

The Hotel Manager is like the **Hypervisor**.

---

# 💻 Practical Example

Suppose a company owns one physical server.

```
CPU = 64 Cores

RAM = 256 GB

Storage = 8 TB
```

The Hypervisor creates:

```
VM 1

Ubuntu

8 vCPU

16 GB RAM

200 GB Storage

--------------------

VM 2

Windows Server

16 vCPU

32 GB RAM

500 GB Storage

--------------------

VM 3

CentOS

12 vCPU

64 GB RAM

1 TB Storage
```

Although all Virtual Machines use the same hardware,

they operate independently.

---

# 🏢 Types of Hypervisors

There are **two types of Hypervisors**.

---

## Type 1 Hypervisor (Bare-Metal Hypervisor)

A Type 1 Hypervisor runs **directly on the physical hardware**.

There is no Host Operating System.

```
Applications

↓

Guest Operating Systems

↓

Hypervisor

↓

Physical Hardware
```

### Advantages

- Better Performance
- Higher Security
- Lower Overhead
- Used in Enterprise Data Centers

### Examples

- VMware ESXi
- Microsoft Hyper-V
- Xen
- KVM

---

## Type 2 Hypervisor (Hosted Hypervisor)

A Type 2 Hypervisor runs **on top of an existing Operating System**.

```
Applications

↓

Guest Operating Systems

↓

Hypervisor

↓

Host Operating System

↓

Physical Hardware
```

### Advantages

- Easy to Install
- Good for Learning
- Good for Development
- Suitable for Personal Computers

### Examples

- Oracle VirtualBox
- VMware Workstation
- VMware Fusion
- Parallels Desktop

---

# 🎤 Interview Answer

A Hypervisor is software that creates and manages Virtual Machines by sharing the physical hardware among multiple operating systems. It allocates virtual resources, isolates Virtual Machines from one another, and enables multiple operating systems to run simultaneously on a single physical server.

---

# ⭐ Key Points

- Hypervisor enables Virtualization.
- It creates and manages Virtual Machines.
- It allocates hardware resources.
- It provides isolation.
- It improves hardware utilization.
- There are two types of Hypervisors.

---

# ❌ Common Mistakes

### ❌ Hypervisor is an Operating System.

✅ Wrong.

A Hypervisor is software that manages Virtual Machines.

---

### ❌ Every Hypervisor requires Windows.

✅ Wrong.

Many enterprise Hypervisors run directly on hardware.

---

### ❌ Hypervisor creates physical servers.

✅ Wrong.

It creates **Virtual Machines**.

---

# 🧠 Interview Deep Dive

## Why is a Hypervisor required?

Because physical hardware cannot be safely shared among multiple operating systems without a management layer.

The Hypervisor performs that management.

---

## Why are enterprise companies using Type 1 Hypervisors?

Because they provide:

- Better performance
- Better resource utilization
- Better security
- Lower overhead

---

## Why do students usually use Type 2 Hypervisors?

Because they are:

- Easy to install
- Free (VirtualBox)
- Run on Windows, Linux, and macOS
- Perfect for learning

---

# ❓ Frequently Asked Interview Questions

### Q1. What is a Hypervisor?

A Hypervisor is software that creates and manages Virtual Machines.

---

### Q2. What is another name for Hypervisor?

Virtual Machine Monitor (VMM).

---

### Q3. What are the two types of Hypervisors?

- Type 1 (Bare-Metal)
- Type 2 (Hosted)

---

### Q4. Which Hypervisor is used in enterprises?

Type 1 Hypervisors.

---

### Q5. Which Hypervisor is commonly used by students?

Type 2 Hypervisors such as Oracle VirtualBox and VMware Workstation.

---

# 🧩 Connection to Docker

Hypervisors solved many infrastructure problems by allowing multiple Virtual Machines to share one physical server.

However, every Virtual Machine still required:

- Its own Operating System
- Its own Kernel
- Its own System Files

As more Virtual Machines were created, resource usage increased significantly.

This raised an important question:

> **Can we isolate applications without installing a complete Operating System every time?**

That question eventually led to **Containers** and later **Docker**.

---

# 📝 Summary

A Hypervisor is the software responsible for virtualization.

It sits between the physical hardware and Virtual Machines, allowing multiple operating systems to safely share the same server.

Hypervisors improve hardware utilization, provide isolation, and make virtualization possible.

They are the foundation of modern cloud computing and enterprise virtualization.