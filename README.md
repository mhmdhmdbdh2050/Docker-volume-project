# ��� Docker Volume Persistence Project

A hands-on Docker project demonstrating how Docker Volumes provide persistent storage for containers.

This project proves that data stored inside a Docker Volume remains available even after deleting the container that created it.

---

# ��� Project Objective

The goal of this project is to understand how Docker Volumes work by creating a practical example.

We will:

- Create a Docker Volume
- Attach the Volume to a container
- Store data inside the Volume
- Delete the container
- Create a new container
- Reuse the same Volume
- Verify that the data still exists

---

# ��� Project Architecture

```

Docker Host
│
├── Docker Volume (my-volume)
│
├── Container 1
│ │
│ └── Creates file.txt
│
└── Container 2
│
└── Reads file.txt

```

The Docker Volume exists independently from containers.

Containers can be created or deleted without affecting the stored data.

---

# ��� Project Structure

```

docker-volume-project/
│
├── README.md
├── .gitignore
│
└── screenshots/
├── Docker-volume-1.jpg
├── Docker-volume-2.jpg
├── Docker-volume-3.jpg
├── Docker-volume-4.jpg
├── Docker-volume-5.jpg
├── Docker-volume-6.jpg
├── Docker-volume-7.jpg
└── Docker-volume-8.jpg

```

---

# ��� Technologies Used

- Docker
- Docker Volume
- Ubuntu Container
- Git
- GitHub
- Git Bash

---

# ��� Project Screenshots

## 1. Docker Volume Created

![Docker Volume](screenshots/Docker-volume-1.jpg)

---

## 2. Running First Container

![Container 1](screenshots/Docker-volume-2.jpg)

---

## 3. Creating file.txt inside the Volume

![Create File](screenshots/Docker-volume-3.jpg)

---

## 4. Reading the File

![Read File](screenshots/Docker-volume-4.jpg)

---

## 5. Second Container Using the Same Volume

![Container 2](screenshots/Docker-volume-5.jpg)

---

## 6. Data Persistence Verification

![Persistence](screenshots/Docker-volume-6.jpg)

---

## 7. Volume In Use Error

![Volume Error](screenshots/Docker-volume-7.jpg)

---

## 8. Final Result

![Final Result](screenshots/Docker-volume-8.jpg)
# ⚙️ Step-by-Step Implementation

## Step 1 - Create the Project Folder

Create a new project directory.

```bash
mkdir docker-volume-project
cd docker-volume-project
```

---

## Step 2 - Initialize Git

Initialize a Git repository.

```bash
git init

git branch -M main
```

This allows us to track project files and upload the project to GitHub later.

---

## Step 3 - Create Docker Volume

Create a new Docker Volume.

```bash
docker volume create my-volume
```

Verify it exists.

```bash
docker volume ls
```

Expected output:

```
local my-volume
```

---

## Step 4 - Inspect the Volume

Display detailed information.

```bash
docker volume inspect my-volume
```

Docker shows:

- Volume Name
- Driver
- Mount Point
- Labels
- Scope

The Mountpoint is where Docker stores the data on the host.

---

## Step 5 - Run the First Container

Create an Ubuntu container and attach the volume.

```bash
docker run -it --name volume-container-1 -v my-volume:/data ubuntu bash
```

Explanation:

- `-it` → Interactive terminal
- `--name` → Container name
- `-v` → Attach Docker Volume
- `/data` → Mount point inside the container

---

## Step 6 - Store Data Inside the Volume

Move to the mounted directory.

```bash
cd /data
```

Create a file.

```bash
echo "Hello from Docker Volume" > file.txt
```

Read the file.

```bash
cat file.txt
```

Result:

```
Hello from Docker Volume
```

At this point the file is stored inside the Docker Volume.

---

## Step 7 - Delete the Container

Exit the container.

```bash
exit
```

Delete it.

```bash
docker rm -f volume-container-1
```

Although the container is removed, the Docker Volume still exists.

---

## Step 8 - Create a New Container

Run another Ubuntu container using the same Docker Volume.

```bash
docker run -it --name volume-container-2 -v my-volume:/data ubuntu bash
```

Enter the mounted directory.

```bash
cd /data
```

List files.

```bash
ls -l
```

Read the file.

```bash
cat file.txt
```

The same file is still available.

This proves Docker Volumes provide persistent storage.

---

## Step 9 - Remove the Volume

Trying to remove the volume while it is still attached produces an error.

```bash
docker volume rm my-volume
```

Docker responds:

```
volume is in use
```

Delete the container first.

```bash
docker rm -f volume-container-2
```

Now remove the volume.

```bash
docker volume rm my-volume
```

Verify removal.

```bash
docker volume ls
```

The volume is no longer listed.

---

# ✅ What This Project Demonstrates

- Creating Docker Volumes
- Attaching Volumes to Containers
- Persistent Storage
- Sharing Data Between Containers
- Volume Lifecycle Management
- Git Project Structure
- GitHub Documentation
# ⚠️ Errors We Faced

## 1. Wrong Directory Name

Initially, the command was written incorrectly:

## 1. Docker Volume Is In Use

When trying to remove the volume:

```bash
docker volume rm my-volume
```

Docker returned:

```
Error response from daemon:
remove my-volume: volume is in use
```

### Reason

The Docker Volume was still attached to an existing container.

### Solution

Delete the container first:

```bash
docker rm -f volume-container-2
```

Then remove the volume:

```bash
docker volume rm my-volume
```

---

## Q1: What is a Docker Volume?

A Docker Volume is Docker's preferred mechanism for storing persistent data outside the container filesystem.

---

## Q2: Why use Docker Volumes?

- Persistent storage
- Data sharing between containers
- Better performance
- Easier backup and restore

---

## Q3: Does deleting a container delete the volume?

No.

Deleting a container does **not** remove the Docker Volume.

---

## Q4: Can multiple containers use the same volume?

Yes.

## Q5: Why couldn't Docker remove the volume?

Because it was still attached to an existing container.

Docker protects the volume until no containers are using it.
---

# ��� Conclusion

This project provides a practical demonstration of Docker Volume persistence.

Unlike container storage, Docker Volumes continue to exist even after containers are removed, making them the recommended solution for databases, application data, logs, and any files that must survive survive the container lifecycle.

