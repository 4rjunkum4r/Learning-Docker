# 19 - Dockerfile

## What is a Dockerfile?

A **Dockerfile** is a plain text file that contains a set of instructions used by Docker to automatically build a Docker image.

Instead of manually creating a container, installing software, configuring it, and then saving it as an image, we write all those steps inside a Dockerfile. Docker reads these instructions one by one and creates the image automatically.

In simple words:

> **Dockerfile = Recipe**
>
> **Docker Image = Final Dish**

---

## Why do we need a Dockerfile?

Without a Dockerfile, creating an image would require performing every step manually.

For example:

- Pull an Ubuntu image
- Start a container
- Install required packages
- Copy application files
- Configure the application
- Commit the container as an image

This process is repetitive and error-prone.

A Dockerfile automates all these steps so that anyone can build the exact same image with a single command.

---

## How Docker Builds an Image

Docker uses the following command:

```bash
docker build
```

This command:

1. Reads the Dockerfile.
2. Executes every instruction one by one.
3. Creates a Docker image.

Example:

```text
Dockerfile
     │
     ▼
docker build
     │
     ▼
Docker Image
```

---

# Basic Dockerfile Example

```dockerfile
FROM ubuntu

RUN apt-get update

CMD ["echo", "Hello from Docker"]
```

When Docker runs:

```bash
docker build .
```

it reads every instruction in the Dockerfile and builds a Docker image.

---

# Dockerfile Instructions

A Dockerfile is made up of multiple instructions.

Some commonly used instructions are:

- FROM
- RUN
- COPY
- ADD
- WORKDIR
- ENV
- EXPOSE
- CMD
- ENTRYPOINT

In this lesson we mainly learned:

- FROM
- RUN
- CMD

---

# FROM Instruction

The **FROM** instruction specifies the **base image** for the Dockerfile.

Syntax:

```dockerfile
FROM <image>:<tag>
```

Example:

```dockerfile
FROM ubuntu
```

or

```dockerfile
FROM ubuntu:24.04
```

### What does FROM do?

It tells Docker:

> "Start building my image using this existing image."

Every instruction written after `FROM` is applied on top of this base image.

Example:

```dockerfile
FROM ubuntu

RUN apt-get update

RUN apt-get install -y git
```

Here,

- Base image = Ubuntu
- Update Ubuntu
- Install Git on Ubuntu

Everything happens on top of the Ubuntu image.

---

# Docker Image Layers

One important concept I learned is that **Docker images are made of multiple layers.**

Almost every Dockerfile instruction creates a new layer.

Example Dockerfile:

```dockerfile
FROM ubuntu

MAINTAINER John Doe

RUN apt-get update

CMD ["echo","Hello from DolphinED"]
```

Docker internally creates layers like:

```
Layer 1
FROM ubuntu

↓

Layer 2
MAINTAINER John Doe

↓

Layer 3
RUN apt-get update

↓

Layer 4
CMD ["echo","Hello from DolphinED"]
```

Each instruction maps to its own layer inside the Docker image.

So the final Docker image is actually a stack of multiple layers.

This layered architecture is one of the reasons Docker is fast and efficient because unchanged layers can be reused from cache.

---

# RUN Instruction

The **RUN** instruction executes commands while the image is being built.

Syntax:

```dockerfile
RUN <command>
```

Example:

```dockerfile
RUN apt-get update
```

or

```dockerfile
RUN apt-get install -y vim
```

The command is executed during **image build time**, not when the container starts.

---

## Multiple RUN Commands

Example:

```dockerfile
RUN apt-get update

RUN apt-get install -y vim
```

This creates **two separate layers**.

```
Layer 1
FROM ubuntu

↓

Layer 2
RUN apt-get update

↓

Layer 3
RUN apt-get install -y vim
```

Although it works, it is **not recommended** because it creates unnecessary layers.

---

# Optimizing Image Layers

A better approach is to combine commands into a single RUN instruction.

Example:

```dockerfile
RUN apt-get update && \
    apt-get install -y vim git
```

Now Docker creates only **one layer** for both commands.

Benefits:

- Smaller image
- Fewer layers
- Faster builds
- Better caching

This is considered a best practice.

---

# Viewing Docker Image Layers

Docker provides a command to inspect image layers.

```bash
docker history <image-name>
```

Example:

```bash
docker history ubuntu
```

This command displays:

- Image layers
- Commands used
- Layer sizes
- Creation time

---

# CMD Instruction

The **CMD** instruction specifies the default command that runs when the container starts.

Syntax:

```dockerfile
CMD ["executable", "param1", "param2"]
```

Example:

```dockerfile
CMD ["echo","Hello from Docker"]
```

When the container starts, it prints:

```
Hello from Docker
```

Another example:

```dockerfile
CMD ["python","app.py"]
```

When the container starts, Docker executes:

```bash
python app.py
```

---

## Important Rule About CMD

A Dockerfile should contain **only one CMD instruction**.

Example:

```dockerfile
CMD ["echo","Hello"]

CMD ["python","app.py"]
```

Only the **last CMD** will be used.

Docker ignores the earlier CMD instructions.

---

# CMD vs RUN

| RUN | CMD |
|------|------|
| Executes during image build | Executes when the container starts |
| Used to install packages or configure the image | Used to define the default startup command |
| Creates image layers | Does not create build layers for installation |
| Runs only while building | Runs every time the container starts |

Remember:

- **RUN = Build Time**
- **CMD = Run Time**

---

# docker build Command

Docker builds images using:

```bash
docker build [OPTIONS] PATH
```

Example:

```bash
docker build -t myapp .
```

Explanation:

- `docker build` → Build a Docker image.
- `-t myapp` → Assign the image the name `myapp`.
- `.` → Current directory is the **build context**.

Docker automatically looks for a file named:

```
Dockerfile
```

inside the build context.

---

# Build Context

The **build context** is the directory that Docker can access while building the image.

Example:

```bash
docker build .
```

Here,

```
.
```

means:

> Use the current directory as the build context.

Docker can access:

- Dockerfile
- Source code
- Configuration files
- Any other files inside this directory

---

# Key Points

- A Dockerfile is a text file containing instructions to build a Docker image.
- `docker build` reads the Dockerfile and creates the image.
- `FROM` defines the base image.
- Every instruction after `FROM` is applied on that base image.
- Docker images are made of multiple layers.
- Most Dockerfile instructions create separate layers.
- `RUN` executes commands during image build.
- Multiple RUN instructions create multiple layers.
- Combining commands into one RUN reduces the number of layers and is recommended.
- `docker history <image>` shows the layers of an image.
- `CMD` specifies the default command executed when the container starts.
- Only the last CMD instruction is used.
- `RUN` works at build time, while `CMD` works at runtime.
- `docker build -t image_name .` builds an image from the Dockerfile in the current directory.
- The current directory (`.`) is called the **build context**.

---

# My Understanding

A Dockerfile is simply a **recipe for creating Docker images**.

Instead of manually configuring a container every time, we write all the required steps in a Dockerfile. Docker reads those instructions one by one, creates image layers, and finally produces a reusable Docker image.

I also learned that Docker images are layered. Most Dockerfile instructions create a separate layer, which is why combining related commands into a single `RUN` instruction is considered a best practice. Finally, I understood the difference between `RUN` (build time) and `CMD` (container runtime), which is one of the most important concepts in Docker.