# Java CI/CD Pipeline Project

This project demonstrates a complete end-to-end CI/CD pipeline for a Java Spring Boot web application using Jenkins, Docker, GitHub, and AWS EC2.

The goal of this project is to show how source code can be automatically built, containerized, and deployed to a live server whenever a change is pushed to GitHub.

---

## Tech Stack

- Java 17 
- Spring Boot 
- Maven 
- GitHub 
- Jenkin 
- Docker 
- Docker Hub 
- AWS EC2 (Ubuntu 22.04)

---

## Architecture Overview

GitHub → Jenkins → Maven Build → Docker Build → Docker Hub → EC2 Deployment → Live Web App

Every code push to GitHub triggers Jenkins automatically through a webhook. Jenkins then builds the application, creates a Docker image, pushes it to Docker Hub, and deploys the latest version to an AWS EC2 instance.

---

## CI/CD Pipeline Stages

1. Checkout source code from GitHub 
2. Build Java application using Maven 
3. Build Docker image 
4. Push Docker image to Docker Hub 
5. Deploy container to AWS EC2 using SSH 

All stages are defined inside a `Jenkinsfile` stored in this repository.

---

## Application

The application is a Spring Boot web app with two routes:

- `/` → Home page 
- `/about` → Project information 

It is packaged as a Docker container and runs on AWS EC2.

---

## Proof of Work

Each phase of the project is documented with screenshots inside the Screenshot directorie of this GitHub repository for verification and review.
