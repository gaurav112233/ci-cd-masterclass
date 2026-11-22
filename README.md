
## Architecture

This project implements an automated CI/CD pipeline using
GitHub Actions, Docker, Docker Hub and AWS EC2.


```mermaid
flowchart TD
    A["Developer"] -->|"Git Push"| B["GitHub Repository"]

  B -->|"Push Trigger"| C["GitHub Actions"]

  subgraph CI["Continuous Integration - GitHub Actions Runner"]
        C --> D["Checkout Source Code"]
        D --> E["Setup Java"]
        E --> F["Build Spring Boot Application"]
        F --> G["Generate JAR File"]
        G --> H["Build Docker Image"]
        H --> I["Push Docker Image to Docker Hub"]
    end

   subgraph CD["Continuous Deployment"]
        I --> J["SSH Connection to AWS EC2"]
        J --> K["Pull Latest Docker Image"]
        K --> L["Stop and Remove Old Container"]
        L --> M["Run New Docker Container"]
    end

   M --> N["Spring Boot Application Running on EC2"]
   N --> O["Access /api/welcome Endpoint"]

  style CI fill:#dbeafe,stroke:#2563eb,color:#111827
  style CD fill:#dcfce7,stroke:#16a34a,color:#111827
…





## Project Overview

This project demonstrates an end-to-end CI/CD pipeline for a Java Spring Boot application using GitHub Actions, Docker, Docker Hub and AWS EC2.

The application is automatically built and packaged into a JAR file. GitHub Actions then builds a Docker image and pushes it to Docker Hub.

Using SSH, GitHub Actions connects to the AWS EC2 instance, pulls the latest Docker image, replaces the existing container and starts the updated application.

**Key features:**
- Automated application build using Maven.
- Docker image creation and publishing.
- GitHub Actions workflow triggered by code pushes.
- Secure SSH-based deployment to AWS EC2.
- Containerized Spring Boot application.

**Application endpoint:**

`http://<EC2-PUBLIC-IP>:8080/api/welcome`

Replace the placeholder with your EC2 public IP.
