# 🚀 FastAPI Dockerized Application

This project provides a lightweight and secure Docker setup for running a FastAPI application using Python.

## 📦 Features
- Uses **Python 3.11.4 Slim** for minimal footprint.
- Non-privileged user for enhanced security.
- **Efficient caching** for dependency installation.
- **Buffered logging disabled** to ensure real-time logs.
- Runs with **Uvicorn** for high-performance ASGI serving.

## 📜 Requirements
- [Docker](https://www.docker.com/get-started) installed on your system.

## 🚀 Getting Started
### 1️⃣ Build the Docker Image
```sh
docker build -t my-fastapi-app .
```

### 2️⃣ Run the Container
```sh
docker run -p 8001:8001 my-fastapi-app
```

### 3️⃣ Access the Application
Visit `http://localhost:8001` in your browser or use:
```sh
curl http://localhost:8001
```

## 🛠️ Dockerfile Breakdown
### Base Image
```dockerfile
FROM python:3.11.4-slim as base
```
- Uses the **slim** variant for a minimal and secure Python environment.

### Environment Variables
```dockerfile
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
```
- Prevents Python from generating `.pyc` files.
- Ensures logs are output in real-time.

### Dependencies Handling
```dockerfile
RUN --mount=type=cache,target=/root/.cache/pip \
    --mount=type=bind,source=requirements.txt,target=requirements.txt \
    python -m pip install -r requirements.txt
```
- Uses Docker cache and bind mounts to speed up dependency installation.

### Security Considerations
```dockerfile
ARG UID=10001
RUN adduser --disabled-password --gecos "" --home "/nonexistent" --shell "/sbin/nologin" --no-create-home --uid "${UID}" appuser
```
- Runs the application under a **non-root user** for security.

### Running the App
```dockerfile
CMD python3 -m uvicorn app:app --host=0.0.0.0 --port=8001
```
- Runs **Uvicorn**, an ASGI server optimized for FastAPI.

## 📌 Notes
- Modify `requirements.txt` to include necessary dependencies.
- Ensure the `app` module is properly set up in your project.

## 📜 License
This project is licensed under the MIT License.



## Simple python docker dev example for the official docker docs
https://docs.docker.com/language/python/develop/
