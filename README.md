# Flask App CI/CD Pipeline with Jenkins and Docker

A minimal Python Flask web application containerized with Docker and automated through a Jenkins CI/CD pipeline. The app serves a simple "Hello World" HTTP endpoint and is built on a lightweight `python:3.8-slim` base image. The Jenkins pipeline automates the full deployment lifecycle — triggered on every GitHub push — covering code checkout, Docker image build, cleanup of any running containers, and redeployment of the updated container on port 8081.

---

## Project Structure

```
├── app.py              # Flask application
├── requirements.txt    # Python dependencies
├── dockerfile          # Docker image definition
└── Jenkinsfile         # Jenkins CI/CD pipeline
```

---

## Prerequisites

- Python 3.8+
- Docker
- Jenkins (with GitHub plugin)

---

## Getting Started

### Run Locally

```bash
pip install -r requirements.txt
python app.py
```

The app will be available at: `http://localhost:5000`

### Run with Docker

```bash
docker build -t flask-app .
docker run -d -p 5000:5000 flask-app
```

The app will be available at: `http://localhost:5000`

---

## Jenkins CI/CD Pipeline

The `Jenkinsfile` defines an automated pipeline with the following stages:

| Stage | Description |
|---|---|
| **Checkout Code** | Pulls the latest code from the `main` branch on GitHub |
| **Check Docker** | Verifies Docker is available on the Jenkins agent |
| **Build Docker Image** | Builds the Docker image tagged as `venkatesh/jenkins-project3` |
| **Stop Old Container** | Stops and removes any previously running container |
| **Run Container** | Deploys the new container, exposed on port `8081` |

### Trigger

The pipeline is triggered automatically on every **GitHub push** via the `githubPush()` trigger.

### Environment Variables

| Variable | Value |
|---|---|
| `IMAGE_NAME` | `venkatesh/jenkins-project3` |
| `CONTAINER_NAME` | `jenkins-project3-container` |
| `REPO_URL` | `https://github.com/venkatesh-db/jenkins-project3.git` |

---

## API Endpoint

| Method | Route | Response |
|---|---|---|
| GET | `/` | `Hello World` |

---

## Tech Stack

- **Python** — Application runtime
- **Flask** — Web framework
- **Docker** — Containerization (`python:3.8-slim`)
- **Jenkins** — CI/CD automation
- **GitHub** — Source control & pipeline trigger
