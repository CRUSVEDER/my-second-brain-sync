---
title: 9. Docker on Linux
date: 2024-12-07
draft: 
Toc: true
tags:
  - basic
---

---

### *Docker on Linux and Windows: Setting Up and Running Your First Container with Real-Life Use Case*

Docker has revolutionized how we deploy and manage applications, offering a consistent environment across various platforms. By creating containers, Docker allows developers and sysadmins to package their applications with all the dependencies they need, ensuring they run smoothly regardless of the environment. Whether you’re on Linux or Windows, setting up Docker and understanding its core concepts will make your life easier. In this blog, we’ll not only go through the installation process on both Linux and Windows but also dive into a real-life use case—deploying a web application using Docker.

---

### **1. What is Docker?**

Docker is a platform that enables developers to automate the deployment of applications in lightweight, portable containers. These containers include everything the application needs to run, such as libraries, configurations, and runtime environments. Since containers isolate applications from the host system, they ensure that the application runs consistently in any environment, whether it's on a developer's laptop, a staging server, or a production cloud instance.

By using Docker, developers can avoid "it works on my machine" issues because the container behaves the same way across all environments. Containers are fast, isolated, and efficient compared to traditional virtual machines because they share the host system's operating system kernel rather than running a full OS.

---

### **2. Docker Architecture at a Glance**

- **Docker Daemon**: A background service that manages Docker containers, images, networks, and volumes.
- **Docker CLI**: The command-line tool you use to interact with the Docker daemon.
- **Docker Images**: Immutable snapshots that contain the application code and environment necessary to run an application.
- **Docker Containers**: Running instances of Docker images that provide an isolated environment for the application.

---

### **3. Installing Docker on Linux (Ubuntu)**

To run Docker on Linux, we'll use Ubuntu as our base system for this guide. If you're using another distribution, the installation steps are similar but may differ in package managers and repositories.

#### **Step-by-Step Guide to Install Docker on Ubuntu:**

1. **Update your system:** Before installing Docker, ensure that your package list is updated:
    
    ```bash
    sudo apt-get update
    ```
    
2. **Install dependencies:** Docker requires some additional dependencies:
    
    ```bash
    sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
    ```
    
3. **Add Docker’s official GPG key:** Docker packages are signed, and you need to ensure their authenticity:
    
    ```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```
    
4. **Add Docker’s official repository:**
    
    Add the Docker repository for Ubuntu:
    
    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```
    
5. **Install Docker:**
    
    Update your package list and install Docker:
    
    ```bash
    sudo apt-get update
    sudo apt-get install docker-ce
    ```
    
6. **Verify the installation:**
    
    Check if Docker is running:
    
    ```bash
    sudo systemctl status docker
    ```
    

---

### **4. Installing Docker on Windows (Windows 10/11)**

Docker Desktop is the easiest way to install Docker on Windows. It provides a native Docker experience by using **WSL 2** (Windows Subsystem for Linux version 2) and Hyper-V.

#### **Step-by-Step Guide to Install Docker on Windows:**

1. **Download Docker Desktop:**
    
    Go to [Docker’s website](https://www.docker.com/products/docker-desktop) and download Docker Desktop for Windows.
    
2. **Install Docker Desktop:**
    
    Run the installer and follow the on-screen instructions. Docker Desktop will install Docker Engine, Docker CLI, Docker Compose, and Kubernetes.
    
3. **Enable WSL 2:**
    
    Docker Desktop requires WSL 2 to run Linux containers on Windows. If you don’t have it installed, Docker will guide you through the installation process.
    
4. **Run Docker Desktop:**
    
    After installation, launch Docker Desktop from the Start menu. Docker will start the Docker daemon in the background.
    
5. **Verify Docker Installation:**
    
    Open a terminal (PowerShell or Command Prompt) and run:
    
    ```bash
    docker --version
    ```
    
    This will confirm if Docker is correctly installed.
    

---

### **5. Running Your First Docker Container**

Once Docker is installed, let’s run a simple container to verify that everything is working.

#### **Run the Hello World Container:**

In your terminal (Linux or Windows), run the following command:

```bash
docker run hello-world
```

This command pulls the `hello-world` image from Docker Hub (if not already on your system) and runs it in a container. You should see a message that confirms Docker is installed and working correctly:

```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

---

### **6. Real-Life Use Case: Deploying a Web Application Using Docker**

Let’s move beyond the basics and work on a real-world scenario. We will deploy a simple **Flask web application** inside a Docker container. Flask is a lightweight Python web framework.

#### **Step 1: Create a Simple Flask Application**

First, let's create a small Flask application. Create a directory called `flask-app` and navigate into it:

```bash
mkdir flask-app
cd flask-app
```

Inside `flask-app`, create a file called `app.py` with the following content:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, Docker World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

This simple web application will return "Hello, Docker World!" when you visit the home page.

#### **Step 2: Create a Dockerfile**

Next, we’ll need a `Dockerfile` to tell Docker how to build the container image for our Flask application. Create a file named `Dockerfile` inside the `flask-app` directory with the following content:

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container
COPY . /app

# Install Flask in the container
RUN pip install --no-cache-dir -r requirements.txt

# Expose port 5000 for the Flask app
EXPOSE 5000

# Define environment variable for Flask
ENV FLASK_APP=app.py

# Run the Flask app
CMD ["flask", "run", "--host=0.0.0.0"]
```

This Dockerfile does the following:

- Starts from a lightweight Python image (`python:3.8-slim`).
- Sets the working directory to `/app`.
- Copies the Flask application into the container.
- Installs the required Python dependencies (Flask in this case).
- Exposes port `5000` to allow access to the Flask app.
- Runs the Flask app when the container starts.

#### **Step 3: Create the `requirements.txt` File**

Next, create a `requirements.txt` file to list the dependencies. In this case, we only need Flask:

```
Flask==2.0.1
```

#### **Step 4: Build the Docker Image**

Now that we have our Flask app, Dockerfile, and `requirements.txt` ready, let’s build the Docker image. Run the following command inside the `flask-app` directory:

```bash
docker build -t flask-app .
```

This command tells Docker to build an image named `flask-app` using the current directory (denoted by `.`) as the build context.

#### **Step 5: Run the Docker Container**

After the image is built, you can run it using the following command:

```bash
docker run -p 5000:5000 flask-app
```

This command runs the `flask-app` container and maps port `5000` on your local machine to port `5000` in the container. Now, open your web browser and visit `http://localhost:5000`. You should see the message:

```
Hello, Docker World!
```

---

### **7. Cleaning Up**

Once you’re done, you can stop and remove the container:

1. **List all running containers**:
    
    ```bash
    docker ps
    ```
    
2. **Stop the container**:
    
    ```bash
    docker stop <container-id>
    ```
    
3. **Remove the container**:
    
    ```bash
    docker rm <container-id>
    ```
    
4. **Remove the image (optional)**:
    
    ```bash
    docker rmi flask-app
    ```
    

---

### **8. Conclusion: Docker Simplifies Development and Deployment**

In this guide, we went from installing Docker on both Linux and Windows to running your first Docker container and deploying a simple Flask web application. Docker allows developers to build and run applications in consistent environments, minimizing the challenges of dependency management and system compatibility.

This real-world use case shows how Docker can be an integral part of the development and deployment pipeline. Whether you're developing on a local machine, collaborating with a team, or deploying to production, Docker containers provide an isolated, lightweight, and efficient way to manage applications across any platform. Happy containerizing!


---