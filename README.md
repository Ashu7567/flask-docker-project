# 🐳 Flask Docker CI/CD Pipeline Project

This project demonstrates a complete CI/CD pipeline for a simple Flask web application using:

- **Flask (Python)**
- **Docker & Docker Compose**
- **GitHub**
- **Jenkins**
- **DockerHub**
- **Remote Server Deployment via SSH**

---

## 📦 Project Structure



flask-docker-project/
   ├── app/ │ 
     ├── app.py │ 
     ├── test_app.py
     ├── requirements.txt
     ├── Dockerfile 
 ├── docker-compose.yml
 ├──Jenkinsfile


---

## 🚀 Features

- Containerized Flask application using Docker
- `docker-compose` for local development
- Unit testing using Pytest
- Jenkins pipeline for:
  - Building Docker Image
  - Running tests
  - Pushing image to DockerHub
  - Deploying to remote server via SSH

---

## 🧰 Requirements

- Docker
- Docker Compose
- GitHub
- Jenkins (running inside Docker)
- DockerHub account
- Remote Linux server with Docker installed

---

## 🔧 How to Run Locally

```bash
# Step into project directory
cd flask-docker-project

# Build and run using Docker Compose
docker-compose up --build


Jenkinsfile defines stages:

Checkout – Pulls code from GitHub

Build Docker Image – Builds the image using Dockerfile

Run Containers – Uses docker-compose to start services

Run Tests – Runs unit tests using Pytest

Push to DockerHub – Pushes the image using Jenkins credentials

Deploy to Server – SSH into remote server and redeploys container






 Jenkins Credentials Required
Create Jenkins credentials with the following:

ID: docker-hub

Type: Username and Password (for DockerHub)




http://<your-server-ip>:5000



Author
Ashish Kumar – GitHub
