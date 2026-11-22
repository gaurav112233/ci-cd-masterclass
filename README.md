# Spring Boot CI/CD Pipeline using GitHub Actions, Docker & AWS EC2

## Project Overview

This project demonstrates an end-to-end CI/CD pipeline for a Spring Boot application using:

- GitHub Actions
- Maven
- Docker
- Docker Hub
- AWS EC2

The pipeline automatically builds the application, creates a Docker image, pushes it to Docker Hub, and deploys the latest version to an AWS EC2 instance.

---

## Architecture

```mermaid
flowchart LR

    A[Developer] -->|Git Push| B[GitHub Repository]

    B -->|Trigger Workflow| C[GitHub Actions]

    subgraph Continuous Integration
        C --> D[Checkout Code]
        D --> E[Setup Java 17]
        E --> F[Maven Build]
        F --> G[Create JAR]
        G --> H[Build Docker Image]
        H --> I[Push to Docker Hub]
    end

    I --> J[(Docker Hub)]

    subgraph Continuous Deployment
        J --> K[SSH to AWS EC2]
        K --> L[Pull Latest Image]
        L --> M[Stop Existing Container]
        M --> N[Remove Old Container]
        N --> O[Run New Container]
    end

    O --> P[Spring Boot App]
    P --> Q[/api/welcome]
```

---

## Tech Stack

- Spring Boot
- Java 17
- Maven
- Docker
- Docker Hub
- GitHub Actions
- AWS EC2
- Linux

---

## CI/CD Workflow

1. Developer pushes code to GitHub.
2. GitHub Actions workflow is triggered.
3. Maven builds the Spring Boot application.
4. Docker image is created.
5. Docker image is pushed to Docker Hub.
6. GitHub Actions connects to AWS EC2 via SSH.
7. EC2 pulls the latest Docker image.
8. Existing container is stopped and removed.
9. New container is launched.
10. Application becomes available through `/api/welcome`.

---

## Application Endpoint

```http
GET /api/welcome
```

Sample Response:

```json
Welcome to Spring Boot CI/CD Pipeline
```

---

## Repository Structure

```
.
├── src/
├── Dockerfile
├── pom.xml
├── .github
│   └── workflows
│       └── deploy.yml
└── README.md
```
