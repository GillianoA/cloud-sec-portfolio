---
title: "Case Study: Zero-Touch DevSecOps Pipeline"
description: "Automated deployment of a containerized React application to Azure using Terraform, Docker and GitHub Actions."
date: 2026-03-14
tags: ["DevSecOps", "Terraform", "Docker", "GitHub Actions", "Azure", "React"]
ShowToc: true
---

## The Objective
To eliminate manual infrastructure provisioning and enforce strict Infrastructure as Code (IaC) principles for application deployment. 

The goal was to build a completely "zero-touch" pipeline where a single code commit automatically provisions the required cloud environment, builds a secure container and deploys the application without human intervention.

---

## The Architecture
**[View the Infrastructure as Code (IaC) repository on GitHub ↗](https://github.com/GillianoA/zero-touch-portfolio)**

This deployment utilizes a modern DevSecOps toolchain to ensure consistency, security and scalability.

1. **Infrastructure as Code (IaC):** **Terraform** is utilized to programmatically define and deploy the Azure infrastructure, ensuring the environment is perfectly reproducible and version-controlled.
2. **Containerization:** The frontend application (built in **React**) is packaged into a **Docker** container, ensuring consistency across local development and cloud production environments.
3. **CI/CD Automation:** **GitHub Actions** serves as the orchestration engine. It authenticates with Azure, executes the Terraform configuration, builds the Docker image and handles the final deployment.

---

## The Execution Flow
The pipeline operates on a strict, automated sequence triggered by code integration:

1. **Commit & Trigger:** Code is pushed to the main branch, triggering the GitHub Actions workflow.
2. **Provisioning (Terraform):** The pipeline authenticates securely with Azure and runs `terraform apply` to provision or update the necessary hosting resources.
3. **Build & Push (Docker):** The React application is built into a lightweight Docker image and pushed to a container registry.
4. **Deployment:** The newly built container is deployed to the Azure environment, making the application live.

---

## The Business Impact
This zero-touch architecture demonstrates a high level of DevSecOps maturity. By removing manual clicking in the Azure portal, the infrastructure becomes fully auditable, highly resilient to configuration drift and capable of rapid, secure scaling.