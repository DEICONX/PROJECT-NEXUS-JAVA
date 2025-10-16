🧩 Project Overview

This project demonstrates a complete Continuous Integration and Continuous Deployment (CI/CD) pipeline for a Java-based web application using AWS EC2, Apache Maven, Sonatype Nexus Repository, and Apache Tomcat.

The primary objective is to automate the process of building, storing, and deploying a Java web application in a structured and repeatable way — ensuring efficiency, scalability, and consistency across environments.

🧱 Key Components
Component	Description
AWS EC2 Instances	Virtual machines used to host the build server, deploy server, and Nexus artifact repository.
Apache Maven	Used for compiling code, managing dependencies, and packaging .war files.
Nexus Repository Manager	Stores versioned .war files and serves as a private artifact repository.
Apache Tomcat	Web application server used to host and test deployed builds.
Ubuntu 24.04 LTS	Linux distribution used for all server setups due to its reliability and strong ecosystem support.
⚙️ Pipeline Flow

Build Server (EC2):
The build server clones the Java project from GitHub, compiles it using Maven, and generates a .war artifact.

Nexus Repository (EC2):
The build server uploads the generated .war file to Nexus, where it is version-controlled and stored securely.

Deploy Server (EC2):
The deploy server downloads the latest .war file from Nexus and deploys it to Tomcat for live testing or production use.

Version Management:
Each new release (e.g., v0.0.1, v0.0.2, v0.0.3) follows the same pipeline, ensuring a reliable version history and quick rollback options.

✅ Benefits

Streamlined CI/CD workflow

Centralized build and deployment management

Versioned and traceable artifact handling

Automated server configuration with minimal manual intervention

Seamless integration between development and deployment stages
🪄 Introduction

This documentation provides a step-by-step guide to setting up a complete Java CI/CD pipeline using AWS EC2, Maven, Nexus Repository Manager, and Tomcat Server.
It walks you through the process of launching servers, building and versioning your Java application, storing artifacts securely, and deploying them efficiently — all in a reproducible cloud environment.
Whether you’re a DevOps beginner or a system administrator, this guide helps you understand the workflow from code commit to live deployment.
