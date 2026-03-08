# Dockerized Application

This project demonstrates how to containerize a Python web application using Docker.  
The application runs using Uvicorn inside a Docker container and can be started using Docker or Docker Compose.

---

## Project Structure

```
dockerized-application/
│
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── main.py
└── .gitignore
```

---

# Running the Project Locally

Follow these steps to run the project on your local machine.

## 1 Clone the Repository

```bash
git clone https://github.com/Kaustubh-goilkar/dockerized-application.git
```

---

## 2 Go to the Project Directory

```bash
cd dockerized-application
```

---

## 3 Start the Application Using Docker Compose

```bash
docker compose up --build
```

This command will:

- Build the Docker image
- Create a container
- Start the application

---

## 4 Access the Application

Open your browser and go to:

```
http://localhost:8000
```

---

## Stop the Application

Press:

```
CTRL + C
```

or run:

```bash
docker compose down
```

---

# Dockerfile

```dockerfile
FROM python:3.10.20-slim

WORKDIR /app

COPY requirements.txt requirements.txt

RUN pip3 install -r requirements.txt

COPY . .

CMD uvicorn main:app --host=0.0.0.0 --port=8000
```

---

# Dockerfile Explanation

## Base Image

```
FROM python:3.10.20-slim
```

Uses the official Python image as the base image.  
The `slim` version is lightweight and reduces the final Docker image size.

---

## Working Directory

```
WORKDIR /app
```

Sets the working directory inside the container to `/app`.

All commands after this will run inside `/app`.

---

## Copy Requirements File

```
COPY requirements.txt requirements.txt
```

Copies the dependency file into the container.

---

## Install Dependencies

```
RUN pip3 install -r requirements.txt
```

Installs all Python dependencies needed by the application.

---

## Copy Application Code

```
COPY . .
```

Copies the entire project into the container.

---

## Start the Application

```
CMD uvicorn main:app --host=0.0.0.0 --port=8000
```

Explanation:

- `main` → Python file (`main.py`)
- `app` → FastAPI application instance
- `0.0.0.0` → Allows access from outside the container
- `8000` → Application port

---

# Docker Compose

Example `docker-compose.yml`:

```yaml
version: "3"

services:
  web:
    build: .
    ports:
      - "8000:8000"
```

---

# Common Docker Commands

These are some frequently used Docker commands.

## List Running Containers

```bash
docker ps
```

Shows all currently running containers.

---

## List All Containers

```bash
docker ps -a
```

Shows all containers including stopped ones.

---

## List Docker Images

```bash
docker images
```

Displays all Docker images stored on your system.

---

## Stop a Container

```bash
docker stop <container_id>
```

Stops a running container.

---

## Remove a Container

```bash
docker rm <container_id>
```

Deletes a container.

---

## Remove an Image

```bash
docker rmi <image_id>
```

Deletes a Docker image.

---

## Build Docker Image

```bash
docker build -t dockerized-application .
```

Builds a Docker image from the Dockerfile.

---

## Run Docker Container

```bash
docker run -p 8000:8000 dockerized-application
```

Runs a container and maps port 8000 from container to local machine.

---

# Useful Docker Documentation

You can find the most commonly used Docker commands here:

Official Docker documentation:

https://docs.docker.com/reference/cli/docker/

Docker cheat sheet:

https://docs.docker.com/get-started/docker_cheatsheet.pdf

---

# Requirements

- Docker installed
- Git installed

---

# .gitignore Example

```
__pycache__/
*.pyc
*.pyo
*.pyd
.env
venv/
.vscode/
.idea/
```

---

# Author

This project demonstrates how to dockerize a Python application for development and deployment using Docker and Docker Compose.
