# Day-1

## **1. Build Images**

```bash
docker build -f 3.cmdDockerfile -t cmd-image .
docker build -f 4.entrypoint -t entrypoint-image .
docker build -f 5.entrypointCmd -t entrypointcmd-image .
docker build -f 6.envDockerfile -t env-image .
docker build -f 7.Addfile -t addfile-image .
docker build -f 8.userDockerfile -t user-image .
```

---

## **2. Check If Images Are Created**

```bash
docker images
```

---

## **3. Create Containers (without running them)**

```bash
docker create --name cmd-container cmd-image
docker create --name entrypoint-container entrypoint-image
docker create --name entrypointcmd-container entrypointcmd-image
docker create --name env-container env-image
docker create --name addfile-container addfile-image
docker create --name user-container user-image
```

---

## **4. Run Containers**

```bash
docker run --name cmd-container-run cmd-image
docker run --name entrypoint-container-run entrypoint-image
docker run --name entrypointcmd-container-run entrypointcmd-image
docker run --name env-container-run env-image
docker run --name addfile-container-run addfile-image
docker run --name user-container-run user-image
```

---

---

# **CMD vs ENTRYPOINT**

Docker provides **CMD** and **ENTRYPOINT** to define what happens when a container starts — but they behave differently.

---

## **1. ENTRYPOINT**

### **Purpose:**

Defines the **main command** that *always* runs when the container starts.

### **Key behavior:**

* Arguments passed in `docker run` **are appended** to the ENTRYPOINT.
* ENTRYPOINT **cannot be overridden** easily (unless you use `--entrypoint`).

### Example:

```dockerfile
ENTRYPOINT ["python3", "app.py"]
```

Running:

```bash
docker run imageName --debug
```

Result:
It runs → `python3 app.py --debug`

---

## **2. CMD**

### **Purpose:**

Provides **default arguments** to either:

* ENTRYPOINT, or
* The default command if no ENTRYPOINT exists.

### **Key behavior:**

* CMD **IS overridden** if you pass arguments to `docker run`.

### Example:

```dockerfile
CMD ["python3", "app.py"]
```

Running:

```bash
docker run imageName test.txt
```

`test.txt` **replaces** the entire CMD.

---

# **COPY vs ADD**

Both COPY and ADD copy files into the image — but ADD has extras.

---

## **1. COPY**

### **Purpose:**

Copy files/directories from host → container.

### **Key behavior:**

* Simple and predictable
* **Only copies files**

### Example:

```dockerfile
COPY src/ /app/
```

---

## **2. ADD**

### **Purpose:**

Copy files like COPY, **but with extra features**.

### **Key behavior:**

* Can **download remote URLs**
* Can **auto-extract `.tar` files**
* More “magic”, less predictable

### Examples:

#### Auto-extracts tar:

```dockerfile
ADD app.tar /app
```

#### Download from URL:

```dockerfile
ADD https://example.com/file.txt /data/
```
