
## 🚀 Node.js Application

### Files
- **Dockerfile**: Simple Node.js container setup
- **.dockerignore**: Excludes unnecessary files from Docker context
- **package.json**: Node.js project configuration
- **app.js**: Simple HTTP server

### Build and Run
```bash
# Build the image
docker build -t node-image .

# Run the container
docker run -p 3000:3000 node-image
```

### Access
Open your browser and go to: `http://localhost:3000`

## ☕ Spring Boot PetClinic Application

### Files

### Features
- Uses OpenJDK 17
- Clones Spring PetClinic from GitHub
- Builds with Maven
- 
### Build Arguments
- `APP_VERSION`: Application version (default: latest)

### Environment Variables
- `SPRING_PROFILES_ACTIVE`: Spring profile (default: production)

### Build and Run
```bash
# Build with default values
docker build -t spring-petclinic .

# Build with custom app version
docker build --build-arg APP_VERSION=v1.0 -t spring-petclinic .

# Run the container
docker run -p 8080:8080 spring-petclinic

# Run with custom environment
docker run -p 8080:8080 -e SPRING_PROFILES_ACTIVE=dev spring-petclinic
```

### Access
Open your browser and go to: `http://localhost:8080`

