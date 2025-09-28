# Catalogue Service - CI Pipeline

This repository contains Jenkins pipeline configurations for the **Catalogue Service** Continuous Integration (CI) process. It automates building, testing, and packaging the microservice to ensure code quality and reliability.

## 🚀 Pipeline Stages
1. **Checkout Code** – Pull source code from GitHub.
2. **Build** – Compile and package the application (Maven/Gradle).
3. **Unit Tests** – Run automated tests to validate functionality.
4. **Static Code Analysis** – Integrate with SonarQube (optional).
5. **Artifact Upload** – Store artifacts in Nexus/Artifactory.
6. **Notifications** – Send build status updates to Slack/Email.