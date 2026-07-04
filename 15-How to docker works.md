# ⚙️ How Docker Works Internally

---

# 📚 Prerequisites

Before learning how Docker works internally, you should understand:

- Docker Overview
- Docker Architecture
- Containers
- Docker Images
- Docker Daemon
- Docker Client
- Linux Processes

---

# 🎯 Learning Objective

We already know the major Docker Architecture components.

Now the question becomes:

> **What happens internally after we type a Docker command?**

For example,

```bash
docker run nginx
```

How does this command eventually create a running container?

Let's understand the complete workflow.

---

# 🏗️ Components Involved

Internally Docker mainly uses four components:

1. Docker CLI
2. Docker Daemon (dockerd)
3. containerd
4. runC

Each component has a different responsibility.

---

# 1️⃣ Docker CLI

## Definition

Docker CLI (Command Line Interface) is the interface through which users interact with Docker.

Whenever we type Docker commands like:

```bash
docker run

docker pull

docker build

docker stop
```

we are using Docker CLI.

Docker CLI itself does **not** create containers.

It simply sends the request to Docker Daemon.

---

## English Explanation

Docker CLI is like a messenger.

It accepts commands from the user and forwards them to Docker Daemon.

It does not perform the actual work.

---

## Hinglish Explanation

Docker CLI wahi terminal hai jisme hum commands likhte hain.

Example:

```bash
docker run nginx
```

CLI sirf command leta hai.

Uske baad command Docker Daemon ko bhej deta hai.

CLI khud container nahi banata.

---

## Interview Answer

Docker CLI is the command-line interface used by developers to communicate with Docker. It accepts Docker commands and forwards them to Docker Daemon.

---

# 2️⃣ Docker Daemon (dockerd)

## Definition

Docker Daemon (`dockerd`) is the heart of Docker.

It runs continuously as a background service.

Every Docker request reaches Docker Daemon first.

---

## Responsibilities

Docker Daemon:

- Receives Docker API requests
- Builds Images
- Runs Containers
- Stops Containers
- Deletes Containers
- Pulls Images
- Pushes Images
- Manages Networks
- Manages Volumes

---

## Communication

Workflow:

```
Docker CLI

↓

Docker Daemon (dockerd)
```

After receiving the request,

Docker Daemon decides what action needs to be performed.

---

## Important Point

Docker Daemon does **not** directly create Linux containers.

Instead,

it delegates container management to **containerd**.

---

## Hinglish Explanation

Dockerd Docker ka brain hai.

Ye background me continuously chalta rehta hai.

Jaise hi command aati hai,

ye decide karta hai kya karna hai.

Lekin actual low-level container creation ye khud nahi karta.

Ye containerd ko instruction deta hai.

---

## Interview Answer

Docker Daemon is the background service that processes Docker API requests and manages Docker resources. It delegates low-level container operations to containerd.

---

# 3️⃣ containerd

## Definition

containerd is an industry-standard container runtime.

It receives requests from Docker Daemon and manages the entire lifecycle of containers.

---

## Responsibilities

containerd manages:

- Containers
- Images
- Storage
- Snapshots
- Networking
- Image Pull
- Image Push

It is responsible for preparing everything required before a container starts.

---

## Important Point

containerd still does **not** create Linux processes itself.

Instead,

it asks **runC** to create the actual container.

---

## Hinglish Explanation

containerd ko manager samjho.

Ye sab prepare karta hai.

- Image ready karta hai.
- Storage manage karta hai.
- Networking prepare karta hai.
- Container lifecycle manage karta hai.

Lekin actual container banana iska kaam nahi hai.

Ye runC ko bolta hai.

---

## Interview Answer

containerd is a container runtime responsible for managing the lifecycle of containers, images, networking, and storage.

---

# 4️⃣ runC

## Definition

runC is a lightweight low-level container runtime.

It actually creates and starts Linux containers.

---

## Responsibilities

runC:

- Creates Containers
- Starts Containers
- Uses Linux Kernel Features
- Creates Linux Processes

---

## How?

runC uses Linux technologies like:

- Namespaces
- Cgroups
- OCI Runtime Specification

to create isolated containers.

---

## Hinglish Explanation

runC sabse niche wala component hai.

Ye actual Linux container banata hai.

Container basically ek isolated Linux process hota hai.

runC hi us process ko create karta hai.

---

## Interview Answer

runC is a low-level OCI-compliant runtime that creates and starts containers using Linux kernel features.

---

# 🧩 Understanding the Complete Flow

Suppose we execute:

```bash
docker run nginx
```

---

## Step 1

Developer types:

```bash
docker run nginx
```

↓

Docker CLI receives the command.

---

## Step 2

Docker CLI sends the request to Docker Daemon.

```
Docker CLI

↓

dockerd
```

---

## Step 3

Docker Daemon checks:

"Do I already have the nginx image?"

If not,

it asks containerd to download it.

---

## Step 4

containerd pulls the required image from Docker Hub.

It also prepares:

- Storage
- Networking
- Snapshots

---

## Step 5

After everything is ready,

containerd asks runC:

> "Create a container from this image."

---

## Step 6

runC creates an isolated Linux Process.

Namespaces and cgroups are configured.

The container starts.

---

## Step 7

Your application is now running.

```
docker run nginx

↓

Docker CLI

↓

Docker Daemon

↓

containerd

↓

runC

↓

Running Container
```

---

# 🧠 Complete Architecture

```
Developer

↓

Docker CLI

↓

Docker Daemon (dockerd)

↓

containerd

↓

runC

↓

Linux Kernel

↓

Running Container
```

---

# 💡 Real-Life Analogy

Imagine building a house.

Customer

↓

Receptionist

↓

Project Manager

↓

Construction Worker

↓

Finished House

Docker is similar.

```
Developer

↓

Docker CLI

↓

Docker Daemon

↓

containerd

↓

runC

↓

Running Container
```

Each component has its own responsibility.

---

# ❌ Common Misconceptions

### Docker CLI creates containers.

❌ Wrong

Docker CLI only sends commands.

---

### Docker Daemon directly creates containers.

❌ Wrong

Docker Daemon delegates the work to containerd.

---

### containerd creates Linux processes.

❌ Not exactly.

containerd prepares everything and asks runC to create the container.

---

### runC manages images.

❌ Wrong.

runC only creates and starts containers.

Image management belongs to containerd.

---

# 🎤 Interview Questions

## Q1. What is Docker CLI?

The command-line interface used to communicate with Docker.

---

## Q2. What is dockerd?

Docker's background service that processes Docker API requests.

---

## Q3. What is containerd?

A container runtime responsible for managing container lifecycle, images, networking, and storage.

---

## Q4. What is runC?

A low-level OCI runtime that creates and starts Linux containers.

---

## Q5. Which component actually creates containers?

**runC** creates the actual Linux container.

---

## Q6. What is the flow after executing `docker run nginx`?

```
Docker CLI

↓

Docker Daemon

↓

containerd

↓

runC

↓

Running Container
```

---

# 📝 Summary

When a developer executes a Docker command, the Docker CLI sends the request to the Docker Daemon (`dockerd`). The Docker Daemon processes the Docker API request and delegates container management to `containerd`. The `containerd` runtime manages images, storage, networking, and the overall container lifecycle. Finally, `runC` uses Linux kernel features to create and start the actual container as an isolated Linux process. This layered architecture makes Docker modular, efficient, and easier to maintain.

---

# 📖 New Terms Learned

- Docker CLI
- Docker Daemon (dockerd)
- Docker API
- containerd
- runC
- OCI Runtime
- Linux Namespaces
- Linux Cgroups
- Container Lifecycle
- OCI Specification