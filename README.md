# Docker Practice and Documentation


## 🐳 Introduction to Docker

Docker is an open-source platform that automates the process of building, deploying, and managing applications within lightweight, portable containers. Containers encapsulate an application and its dependencies, ensuring consistency across different environments and simplifying the deployment process.

### Key Concepts

- **Containers**: Lightweight, standalone, and executable software packages that include everything needed to run an application—code, runtime, libraries, and system tools.
- **Images**: Read-only blueprints for containers that include the application code, libraries, and environment variables. Built from a Dockerfile.
- **Dockerfile**: A text document with instructions to create a Docker image, defining the base image, application code, dependencies, and setup commands.
- **Docker Engine**: The core component that runs and manages Docker containers, consisting of a server, REST API, and command-line interface (CLI).
- **Docker Compose**: A tool for defining and running multi-container Docker applications using a YAML file to configure services, networks, and volumes.

### Benefits of Docker

- **Portability**: Consistent behavior across development, testing, and production environments.
- **Isolation**: Enhanced security and prevention of conflicts between applications.
- **Efficiency**: Lightweight containers with reduced resource overhead and improved startup times.
- **Scalability**: Easy horizontal scaling with multiple container instances.

### Common Use Cases

- **Development**: Consistent environments across the software lifecycle.
- **CI/CD**: Automated and reproducible build, test, and deployment processes.
- **Microservices**: Manage microservices architectures with multiple containers.
- **Legacy Application Modernization**: Simplify migration and integration of legacy applications.

## 🚀 Getting Started

### 1. **Starting a Docker Session**

To initiate a Docker session, use the following command:

```bash
sudo service docker start
```
### 2. Checking Docker Version

To check the installed Docker version, run:

```bash
docker -v
```

### 3. Managing Docker Images

List Docker Images:

```bash
docker images
```

Pull Docker Images from Docker Hub:

```bash
docker pull [Image-Name]
```
### 4. Managing Docker Containers

List Running Containers:

```bash
docker ps
```

List All Containers (including stopped ones):

```bash
docker ps -a
```

Run a New Container:

```bash
docker run [options] [Image-Name]
```

Example of running with environment variables and detached mode:

```bash
docker run --env MYSQL_ROOT_PASSWORD=my-secret-pw -d --name mysql-container mysql
```

Interactive Mode and Detached Mode:

- Run a container interactively and in detached mode:

    ```bash
    docker run --name SampleName -it -d [Image-Name]
    ```
Accessing a Running Container:

- To execute commands inside a running container:
    ```bash
    docker exec -it [container-name/id] /bin/bash
    ```
- Stopping a Running Container:

    ```bash
    docker stop [container-name/id]
    ```
Removing Containers:
- Remove All Containers:

    ```bash
    docker rm -a
    ```

- Remove a Specific Container:

    ```bash
    docker rm [container-id]
    ```

### 5. Managing Docker Images

Remove a Docker Image:

```bash
docker rmi [image-name]
```

### 6. Restarting Containers

To restart a container:

```bash
docker restart [container-name]
```

### 7. Docker Authentication

Docker Login:

```bash
docker login
```

Docker Commit (Create a New Image from a Container):
```bash
docker commit [container-id] [new-image-name]
```

Push Image to Docker Hub:

```bash
docker push [image-name]

```
### 8. Docker Logs

To view logs of a container:

```bash
docker logs [container-name]
```

### 9. Docker Volumes

To manage Docker volumes (persistent storage for containers):

```bash
docker volume [options]

```

# 📦 Creating Custom Docker Images

### 1. Ubuntu Image

**Step 1**: Create a file named Dockerfile with the following content:

```dockerfile
FROM ubuntu
MAINTAINER hardik
RUN apt update
CMD ["echo", "this is my first image"]
```

**Step 2**: Build the Docker image:

```bash
docker build -t myubuntuimage .
```

**Step 3**: List Docker images to verify:
```bash
docker images
```
**Step 4**: Run the created image:

```bash
docker run myubuntuimage
```

### 2. Java Image

**Step 1**: Create a file named `Dockerfile` with the following content:

```dockerfile
FROM openjdk:11
WORKDIR /usr/src/myapp
COPY . /usr/src/myapp/
RUN javac Test.java
CMD ["java", "Test"]
```

Create a file named `Test.java` with the following content:

```java
import java.util.Properties;

public class Test {
  
   public static void printSystemProperties() {
       System.out.println("Printing system properties:");
       Properties props = System.getProperties();
       System.out.println(props);
   }
  
   public static void main(String[] args) {
       System.out.println("Java program started..");
       printSystemProperties();
   }
}
```

**Step 2**: Build the Docker image:

```bash
docker build -t myjavaimage .
```
**Step 3**: Run the created Java image:

```bash
docker run --name javaProject2 myjavaimage
```