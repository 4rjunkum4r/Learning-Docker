# 🏗️ Docker Architecture

---

# 📚 Prerequisites

Before learning Docker Architecture, you should know:

- Why Docker
- Containers
- Containerization
- Docker Overview

---

# 🎯 Learning Objective

Until now we learned:

- What Docker is
- What Containers are
- Why Containers exist

Now the question is:

> **How does Docker actually work internally?**

To understand this, we need to learn Docker Architecture.

---

# 🏛️ Main Components of Docker Architecture

Docker Architecture mainly consists of five components:

1. Docker Client
2. Docker Host
3. Docker Daemon
4. Docker Images
5. Docker Containers
6. Docker Registry

All these components work together to build and run containers.

---

# 1️⃣ Docker Client

## Definition

The Docker Client is the interface through which users interact with Docker.

Whenever we type Docker commands in the terminal, we are using the Docker Client.

Example commands:

```bash
docker build

docker run

docker pull

docker push

docker stop
```

The Docker Client **does not execute these commands itself**.

Instead, it sends every request to the Docker Daemon.

---

## English Explanation

Think of the Docker Client as a remote control.

You press buttons,

but someone else actually performs the work.

Similarly,

you type commands,

and Docker Client forwards those commands to Docker Daemon.

---

## Hinglish Explanation

Docker Client wahi cheez hai jisse hum Docker se baat karte hain.

Jaise hi hum terminal me command likhte hain

```bash
docker run

docker pull

docker build
```

ye command Docker Client receive karta hai.

Docker Client khud kuch execute nahi karta.

Ye request Docker Daemon ko bhej deta hai.

---

## Interview Answer

Docker Client is the command-line interface that allows users to interact with Docker. It accepts Docker commands and forwards them to the Docker Daemon for execution.

---

# 2️⃣ Docker Host

## Definition

The Docker Host is the machine on which Docker Engine is installed.

It can be:

- Laptop
- Desktop
- Physical Server
- Virtual Machine
- Cloud Server

Everything related to Docker runs inside the Docker Host.

---

## Docker Host Contains

- Docker Engine
- Docker Daemon
- Docker Images
- Docker Containers
- Networks
- Volumes

---

## Hinglish Explanation

Host simply matlab

**wo machine jahan Docker install hai.**

Ye machine kuch bhi ho sakti hai.

Example

- Laptop
- AWS EC2
- Azure VM
- Google Cloud VM
- Physical Server

---

## Interview Answer

Docker Host is the machine where Docker Engine is installed and where Docker Images and Containers are managed.

---

# 3️⃣ Docker Daemon (dockerd)

## Definition

Docker Daemon is the heart of Docker.

Its process name is:

```
dockerd
```

It runs continuously in the background as a service.

---

## Responsibilities

Docker Daemon:

- Builds Images
- Runs Containers
- Stops Containers
- Deletes Containers
- Creates Networks
- Creates Volumes
- Pulls Images
- Pushes Images

---

## It Listens to Docker API Requests

Whenever Docker Client sends a command,

Docker Daemon receives it.

Example

```
docker run nginx

↓

Docker Client

↓

Docker Daemon

↓

Run Container
```

---

## Lifecycle Management

Docker Daemon manages the complete lifecycle of containers.

It can

- Start
- Stop
- Restart
- Remove

containers whenever requested.

---

## Registry Communication

Docker Daemon also communicates with Docker Registries.

Example

```
docker pull nginx
```

Daemon contacts Docker Hub,

downloads the image,

stores it locally,

and later creates a container.

---

## Hinglish Explanation

Docker Daemon ko Docker ka brain ya heart bol sakte hain.

Ye background me continuously chalta rehta hai.

Jab hum command dete hain

```
docker run

docker pull

docker build
```

Docker Daemon hi actual kaam karta hai.

---

## Interview Answer

Docker Daemon is the background service that listens for Docker API requests and manages images, containers, networks, and volumes.

---

# 4️⃣ Docker Images

## Definition

Docker Images are read-only templates used to create containers.

Image is basically a blueprint.

It cannot execute itself.

---

## Image Contains

A Docker Image contains

- Application Code
- Libraries
- Runtime
- Dependencies
- Configuration Files
- Environment Variables

Everything required to run an application.

---

## Important Point

One Docker Image

↓

can create

↓

Multiple Containers

Example

```
Image

↓

Container 1

Container 2

Container 3
```

---

## Hinglish Explanation

Image ko ek blueprint ya template samjho.

Image khud run nahi hoti.

Us image se containers bante hain.

---

## Interview Answer

A Docker Image is a read-only template containing everything required to run an application.

---

# 5️⃣ Docker Containers

## Definition

A Docker Container is a running instance of a Docker Image.

Container is where the application actually runs.

---

## Container Contains

A running container includes

- Application
- Runtime
- Dependencies
- Libraries
- Configuration
- Environment Variables

All packaged together.

---

## Important Point

Container runs as an isolated Linux Process.

Each container is independent.

One container crashing usually does not affect others.

---

## Hinglish Explanation

Image blueprint hai.

Container us blueprint se bana hua running application hai.

Simple example

```
Image

↓

docker run

↓

Container

↓

Application Running
```

---

## Interview Answer

A Docker Container is a running instance of a Docker Image that executes the application inside an isolated environment.

---

# 6️⃣ Docker Registry

## Definition

Docker Registry is a storage location where Docker Images are stored.

---

## Public Registry

The most popular registry is

**Docker Hub**

It stores millions of Docker Images.

Example

```
nginx

ubuntu

mysql

postgres

redis
```

---

## Pull

When we need an image,

Docker downloads it from Docker Hub.

Example

```bash
docker pull nginx
```

---

## Push

If we create our own image,

we can upload it.

Example

```bash
docker push myapp:v1
```

---

## Hinglish Explanation

Registry ko image warehouse samjho.

Docker Hub ek public warehouse hai.

Agar image nahi hai

↓

Pull

Agar apni image upload karni hai

↓

Push

---

## Interview Answer

Docker Registry stores Docker Images. Docker Hub is the default public registry from which images can be pulled and to which images can be pushed.

---

# 🔄 Complete Docker Workflow (Connecting the Dots)

This is the complete flow shown in the diagram.

## Step 1

Developer writes

```bash
docker pull nginx
```

↓

Docker Client receives command.

---

## Step 2

Docker Client sends request to Docker Daemon.

---

## Step 3

Docker Daemon checks

"Is the image already available locally?"

---

## Step 4

If NOT

↓

Docker Daemon contacts Docker Registry.

Usually

Docker Hub.

---

## Step 5

Docker Hub sends the Image.

↓

Docker Daemon stores it locally.

---

## Step 6

Now developer runs

```bash
docker run nginx
```

---

## Step 7

Docker Client again sends request to Docker Daemon.

---

## Step 8

Docker Daemon creates a Container from the Image.

---

## Step 9

Container starts.

The application begins running.

---

# 🧠 Real Life Analogy

Imagine ordering food.

Customer

↓

Waiter

↓

Chef

↓

Kitchen

↓

Food

Docker works similarly.

```
Developer

↓

Docker Client

↓

Docker Daemon

↓

Docker Registry (if needed)

↓

Docker Image

↓

Docker Container

↓

Running Application
```

---

# 📊 Complete Architecture Diagram

```
Developer

↓

Docker Client

↓

Docker Daemon (dockerd)

↓

Checks Local Image

↓

Image Exists?

↓

Yes --------------------→ Create Container

↓

No

↓

Docker Hub

↓

Download Image

↓

Store Image

↓

Create Container

↓

Running Application
```

---

# ❌ Common Misconceptions

### Docker Client runs containers.

❌ Wrong

Docker Client only sends commands.

Docker Daemon performs the work.

---

### Image is a running application.

❌ Wrong

Image is only a template.

Container is the running application.

---

### Registry stores Containers.

❌ Wrong

Registry stores Images.

Containers always run on the Docker Host.

---

# 🎤 Interview Questions

## Q1. What is Docker Client?

Interface through which users interact with Docker.

---

## Q2. What is Docker Daemon?

Background service that manages Docker resources.

---

## Q3. What is Docker Host?

Machine where Docker Engine is installed.

---

## Q4. What is Docker Registry?

Storage location for Docker Images.

---

## Q5. What is Docker Hub?

Public Docker Registry.

---

## Q6. Difference between Image and Container?

Image → Blueprint

Container → Running instance of that blueprint.

---

# 📝 Summary

Docker Architecture consists of Docker Client, Docker Host, Docker Daemon, Docker Images, Docker Containers, and Docker Registry. The Docker Client accepts user commands and forwards them to the Docker Daemon. The Docker Daemon performs all operations such as building images, creating containers, pulling images from Docker Hub, and managing the lifecycle of containers. Docker Images act as read-only templates, while Docker Containers are the running instances of those images. Docker Registries such as Docker Hub store images so they can be shared and reused across different environments.

---

# 📖 New Terms Learned

- Docker Client
- Docker Host
- Docker Daemon (dockerd)
- Docker API
- Docker Image
- Docker Container
- Docker Registry
- Docker Hub
- Pull
- Push
- Lifecycle Management