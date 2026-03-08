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

## Dockerfile

```dockerfile
FROM python:3.10.20-slim

WORKDIR /app

COPY requirements.txt requirements.txt

RUN pip3 install -r requirements.txt

COPY . .

CMD uvicorn main:app --host=0.0.0.0 --port=8000
```

---

## Dockerfile Explanation

### Base Image

```
FROM python:3.10.20-slim
```

Uses the official Python image as the base image.  
The `slim` version is lightweight and reduces the overall Docker image size.

---

### Working Directory

```
WORKDIR /app
```

Sets the working directory inside the container to `/app`.

All commands executed after this will run inside this directory.

---

### Copy Requirements File

```
COPY requirements.txt requirements.txt
```

Copies the `requirements.txt` file from the host machine into the container.

---

### Install Dependencies

```
RUN pip3 install -r requirements.txt
```

Installs all Python dependencies listed in the `requirements.txt` file.

---

### Copy Application Code

```
COPY . .
```

Copies all project files from the host machine into the container.

---

### Start the Application

```
CMD uvicorn main:app --host=0.0.0.0 --port=8000
```

Starts the application using Uvicorn.

Explanation:

- `main` → Python file name (`main.py`)
- `app` → FastAPI application instance
- `0.0.0.0` → Allows the container to accept external requests
- `8000` → Application port

---

## Build the Docker Image

Run the following command to build the Docker image:

```
docker build -t dockerized-application .
```

---

## Run the Docker Container

```
docker run -p 8000:8000 dockerized-application
```

This maps:

```
Local Machine : 8000
Container     : 8000
```

You can access the application at:

```
http://localhost:8000
```

---

## Docker Compose

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

## Run Using Docker Compose

Start the application:

```
docker compose up --build
```

Stop the containers:

```
docker compose down
```

---

## Requirements

- Docker
- Python 3.10
- Uvicorn
- FastAPI (if used in the project)

---

## .gitignore Example

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

## Author

This project demonstrates how to dockerize a Python application for development and deployment.
