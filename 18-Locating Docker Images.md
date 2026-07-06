# Locating Docker Images

## Overview

Before Docker can create or run a container, it must first locate the required Docker image.

This process is slightly different depending on whether we use:

- `docker pull`
- `docker run`

The diagram below explains the complete workflow.

---

## Docker Image Lookup Flow

```text
docker run / docker pull
            │
            ▼
Docker looks for the image locally
            │
            ▼
      Is image available?
        │            │
      YES            NO
       │              │
       ▼              ▼
Use local image   Search Docker Hub
                        │
                        ▼
             Is image available?
                 │           │
               YES           NO
                │             │
                ▼             ▼
       Download image     Error:
       to local host      Image not found
                │
                ▼
      Image stored locally
```

---

# What happens when we use `docker pull`?

When we execute:

```bash
docker pull ubuntu
```

Docker performs the following steps:

1. Looks for the image locally.
2. If it already exists, nothing new is downloaded.
3. If it does not exist, Docker searches Docker Hub.
4. If Docker Hub contains the image, Docker downloads it.
5. The downloaded image is stored on the local Docker host for future use.

At this point the process stops.

> **Remember:** `docker pull` only downloads the image. It does **not** create or start any container.

---

# What happens when we use `docker run`?

When we execute:

```bash
docker run ubuntu
```

Docker performs additional steps.

## Step 1

Docker checks whether the image exists on the local Docker host.

---

## Step 2

If the image is not found locally, Docker searches Docker Hub.

---

## Step 3

If the image exists on Docker Hub, Docker downloads it and stores it on the local host.

If the image does not exist, Docker returns:

```text
Error: Image not found
```

---

## Step 4

Once the image is available locally, Docker creates a new container.

Internally, this is similar to executing:

```bash
docker create
```

---

## Step 5

Docker starts the newly created container.

Internally, this is similar to executing:

```bash
docker start
```

---

## Step 6

The container is now running.

---

# Complete Workflow

```text
docker run
      │
      ▼
Check image locally
      │
      ├── Found
      │      │
      │      ▼
      │  Create Container
      │      │
      │      ▼
      │  Start Container
      │
      └── Not Found
             │
             ▼
      Search Docker Hub
             │
      ┌──────┴──────┐
      │             │
     Found       Not Found
      │             │
      ▼             ▼
Download Image   Error:
      │          Image not found
      ▼
Store Image Locally
      │
      ▼
Create Container
      │
      ▼
Start Container
      │
      ▼
Container Running
```

---

# Relationship Between Docker Commands

```text
docker pull
      │
      ▼
Downloads an image only

-----------------------------

docker create
      │
      ▼
Creates a container only

-----------------------------

docker start
      │
      ▼
Starts an existing container

-----------------------------

docker run
      │
      ▼
Pull (if needed)
        +
Create
        +
Start
```

---

# Key Takeaways

✅ `docker pull` only downloads an image.

✅ `docker create` only creates a container.

✅ `docker start` starts an existing container.

✅ `docker run` combines all these operations into a single command.

✅ Downloaded images are stored locally so Docker does not need to download them again unless required.

✅ If Docker cannot find the image locally or on Docker Hub, it returns **"Image not found"**.