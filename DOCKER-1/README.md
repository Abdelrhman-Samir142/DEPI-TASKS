### Saving a Docker Image
```bash
docker save -o node-image.tar node:latest
```

### Loading a Docker Image
```bash
docker load -i node-image.tar
```

## 🛠️ Container Editing Workflow

### Step 1: Build the Image
```bash
docker build -t IMAGE-NAME .
```

### Step 2: Run the Container
```bash
docker run -d -p HOST-PORT:CONTAINER-PORT --name CONTAINER-NAME IMAGE-NAME
```

### Step 3: Access Container Shell
```bash
docker exec -it CONTAINER-NAME bash
```

### Step 4: Navigate and Edit Files
```bash
cd /path/to/files
# Edit files using your preferred editor (nano, vim, etc.)
nano filename.txt
```

## 🌐 Port Configuration 

### Multiple Specific Ports
Run a container with multiple predefined port mappings:
```bash
docker run -d \
  -p 8080:80 \
  -p 8443:443 \
  --name my-container \
  IMAGE-NAME
```

### Random Port Assignment
Let Docker assign random host ports automatically:
```bash
docker run -d \
  -p 80 \
  -p 443 \
  --name my-container \
  IMAGE-NAME
```


---
**Note:** Replace `IMAGE-NAME`, `CONTAINER-NAME`, and port numbers with your specific values.
