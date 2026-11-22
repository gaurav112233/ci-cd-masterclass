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

## CI/CD Architecture

```mermaid
flowchart TD

    A[Developer]
    B[GitHub Repository]
    C[GitHub Actions]

    A -->|Git Push| B
    B -->|Trigger Workflow| C

    subgraph CI["Continuous Integration"]
        D[Checkout Source Code]
        E[Setup Java 17]
        F[Maven Build]
        G[Generate JAR File]
        H[Build Docker Image]
        I[Push Image to Docker Hub]

        D --> E --> F --> G --> H --> I
    end

    C --> D

    J[(Docker Hub)]
    I --> J

    subgraph CD["Continuous Deployment"]
        K[SSH into AWS EC2]
        L[Pull Latest Docker Image]
        M[Stop Existing Container]
        N[Remove Old Container]
        O[Run New Container]

        K --> L --> M --> N --> O
    end

    J --> K

    P[Spring Boot Application Running]
    Q["GET: /api/welcome"]

    O --> P
    P --> Q
```

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
