# Docker

## Overview

Docker is a containerization platform that allows developers and DevOps engineers to package applications and their dependencies into lightweight, portable containers.

Containers provide consistency across development, testing, and production environments.

As part of my DevOps Cloud Engineer journey, I am learning Docker to understand application containerization, deployment, networking, and troubleshooting.


# Why Docker is Important in DevOps

Docker helps DevOps engineers to:

- Package applications consistently
- Reduce environment-related issues
- Create reproducible deployments
- Improve CI/CD workflows
- Run applications using containers
- Prepare workloads for Kubernetes


# Core Concepts Learned

## Container

A container is a lightweight isolated environment that runs an application with required dependencies.


## Image

An image is a read-only template used to create containers.

Example:

Application code + dependencies + runtime = Docker Image


## Dockerfile

A Dockerfile contains instructions to build a Docker image.

Example:

FROM
RUN
COPY
WORKDIR
CMD
EXPOSE


## Registry

A registry stores and distributes Docker images.

Examples:

- Docker Hub
- Amazon ECR


# Docker Commands Practiced

Container management:

- docker run
- docker ps
- docker stop
- docker start
- docker rm


Image management:

- docker build
- docker pull
- docker push
- docker images


Debugging:

- docker logs
- docker exec
- docker inspect


# Docker Networking

Learned:

- Bridge network
- Container communication
- Port mapping
- Exposing applications


Example:

Host Port → Container Port

8080:80


# Docker Storage

Topics covered:

- Volumes
- Bind mounts
- Persistent data


# Docker in DevOps Workflow


Developer Code

↓

Dockerfile

↓

Docker Image

↓

Container

↓

CI/CD Pipeline

↓

Production Deployment


# Hands-on Practice

Practiced:

- Creating Docker images
- Running containers
- Writing Dockerfiles
- Container troubleshooting
- Deploying applications using Docker
