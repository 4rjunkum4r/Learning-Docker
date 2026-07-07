# 20 - Docker Build with Custom Dockerfile (-f) and Build Context

## Why do we use `-f`?

By default, Docker looks for a file named:

```
Dockerfile
```

For example:

```
project/
│
├── Dockerfile
├── app.py
└── requirements.txt
```

Running:

```bash
docker build .
```

Docker automatically uses:

```
project/Dockerfile
```

You don't need to specify its name because Docker already knows to look for a file named **Dockerfile**.

---

# What if my Dockerfile has a different name?

Suppose your folder looks like this:

```
project/
│
├── test.txt
├── app.py
└── requirements.txt
```

Here, there is **no file named Dockerfile**.

Instead, your Dockerfile is named:

```
test.txt
```

Now Docker doesn't know which file contains the Docker instructions.

So you must tell Docker explicitly.

That is what `-f` is for.

Syntax:

```bash
docker build -f <dockerfile-name> .
```

Example:

```bash
docker build -f test.txt .
```

Meaning:

> "Docker, don't use the default Dockerfile.
>
> Instead, use **test.txt** as my Dockerfile."

---

# Understanding the Complete Command

The instructor used:

```bash
docker build -f files/test.txt -t image3 /imagefiles
```

Let's understand every single part.

```
docker build
```

Means:

> Build a Docker image.

---

```
-f
```

Means:

> Use a custom Dockerfile.

---

```
files/test.txt
```

This is **NOT** the build context.

It is the location of the Dockerfile.

Suppose your folders are:

```
project/

├── files/
│      test.txt

└── imagefiles/
       app.py
       package.json
```

Then

```
files/test.txt
```

means

> My Dockerfile is inside the **files** folder.

---

```
-t
```

means

> Tag (name) the image.

---

```
image3
```

This is **NOT a path.**

It is simply the name of the image Docker will create.

Exactly like:

```bash
docker build -t ubuntu-app .
```

Here

```
ubuntu-app
```

is just the image name.

Similarly,

```
image3
```

is only the image name.

After building,

```bash
docker images
```

would show something like

```
REPOSITORY

image3
```

---

```
/imagefiles
```

Now this is the **Build Context**.

This is the folder Docker will send to the Docker daemon.

Docker can only access files inside this folder.

---

# So there are TWO different paths

This is the most important concept.

The command has **two different paths**.

```
docker build -f files/test.txt -t image3 /imagefiles
               ↑                     ↑
         Dockerfile Path       Build Context Path
```

They are completely different.

---

## Path 1

```
files/test.txt
```

Purpose:

> Where is my Dockerfile?

---

## Path 2

```
/imagefiles
```

Purpose:

> Which folder contains all the files needed to build the image?

---

# Visual Example

Suppose your project looks like this:

```
project/

├── files/
│      test.txt
│
└── imagefiles/
       app.py
       requirements.txt
       config.json
```

Command:

```bash
docker build -f files/test.txt -t image3 imagefiles
```

Docker understands:

```
Dockerfile location
↓

files/test.txt

Image name
↓

image3

Build context
↓

imagefiles/
```

---

# Why do we need a Build Context?

Imagine your Dockerfile contains:

```dockerfile
COPY app.py /app/
```

Where is `app.py`?

Docker searches **only inside the Build Context**.

If Build Context is:

```
imagefiles/
```

Docker finds

```
imagefiles/app.py
```

Everything works.

But if Build Context is:

```
files/
```

then

```
files/app.py
```

doesn't exist.

Docker throws an error.

---

# Another Example

Folder structure:

```
project/

Dockerfile

app.py

requirements.txt
```

Command:

```bash
docker build -t myapp .
```

Here

```
Dockerfile
```

is automatically found.

```
.
```

means

Current folder is the Build Context.

---

# Another Example

Folder structure:

```
project/

docker/

    prod.Dockerfile

src/

    app.py

    package.json
```

Command:

```bash
docker build -f docker/prod.Dockerfile -t myapp src
```

Docker interprets this as:

Dockerfile:

```
docker/prod.Dockerfile
```

Image name:

```
myapp
```

Build Context:

```
src/
```

---

# Absolute Path Example

The instructor also showed:

```bash
docker build \
-f /home/ubuntu/apps/imagefiles/test.txt \
-t image3 \
/home/ubuntu/build/contextfiles/app1
```

Let's split it.

```
docker build
```

Build an image.

---

```
-f
```

Custom Dockerfile.

---

```
/home/ubuntu/apps/imagefiles/test.txt
```

Full path to the Dockerfile.

---

```
-t
```

Tag option.

---

```
image3
```

Image name.

---

```
/home/ubuntu/build/contextfiles/app1
```

Build Context.

Docker can access files only inside this folder.

---

# Final Breakdown

```
docker build
```

Build a Docker image.

```
-f
```

Specify a custom Dockerfile.

```
files/test.txt
```

Location of the Dockerfile.

```
-t
```

Tag (name) the image.

```
image3
```

The name of the image being created.

```
/imagefiles
```

The Build Context (folder containing files Docker can use).

---

# One Easy Way to Remember

Think of the command like this:

```
docker build

    Which recipe should I use?
            │
            ▼
     -f files/test.txt

    What should I call the dish?
            │
            ▼
        -t image3

    Which kitchen contains all the ingredients?
            │
            ▼
        imagefiles/
```

- **Recipe** = Dockerfile (`-f files/test.txt`)
- **Dish name** = Image name (`-t image3`)
- **Kitchen** = Build Context (`imagefiles/`)

These are three separate things.

---

# Key Points

- `docker build` starts building a Docker image.
- `-f` tells Docker which file to use as the Dockerfile.
- `files/test.txt` is the path to the Dockerfile.
- `-t` assigns a name (tag) to the image.
- `image3` is the image name, **not** a path.
- `/imagefiles` is the Build Context.
- Yes, the command contains **two different paths**:
  - One for the Dockerfile.
  - One for the Build Context.
- Docker can only access files that exist inside the Build Context.