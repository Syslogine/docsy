---
title: Introduction to Docker for Beginners
linktitle: Docker for Beginners
date: 2024-01-12T12:00:00Z
description: >
  Get started with Docker, the popular containerization platform. Learn the basics of containers, images, and running applications in isolated environments.
tags: ["Docker", "Containerization", "Tutorial", "DevOps"]
categories: ["DevOps", "Docker"]
---

## Prerequisites

Before you begin, ensure that you have Docker installed on your machine. Follow the official [Docker installation guide](https://docs.docker.com/get-docker/) for your operating system.

## Understanding Containers and Images

### What are Containers?

A container is a lightweight, standalone, and executable software package that includes everything needed to run a piece of software, including the code, runtime, libraries, and system tools.

### What are Images?

An image is a lightweight, standalone, and executable software package that includes everything needed to run a container. It serves as the blueprint for containers.

## Basic Docker Commands

### 1. Verify Docker Installation

To ensure Docker is installed, run:

```bash
docker --version
```

### 2. Run Your First Container

Run a simple container:

```bash
docker run hello-world
```

### 3. List Running Containers

View the containers that are currently running:

```bash
docker ps
```

### 4. Explore Docker Images

List the Docker images on your machine:

```bash
docker images
```

## Building and Running Custom Containers

### 1. Create a Dockerfile

Create a file named `Dockerfile` in your project directory:

```Dockerfile
# Use an official Ubuntu runtime as a parent image
FROM ubuntu:20.04

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN apt-get update && apt-get install -y python3

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python3", "app.py"]
```

### 2. Build the Docker Image

Build the Docker image using the Dockerfile:

```bash
docker build -t my-python-app .
```

### 3. Run the Custom Container

Run the container from the built image:

```bash
docker run -p 4000:80 my-python-app
```

Visit [http://localhost:4000](http://localhost:4000) to see your Python application running in a Docker container.

## Conclusion

Congratulations! You've taken your first steps into the world of Docker. This tutorial covered the basics of containers, images, and running custom applications in Docker containers. Dive deeper into Docker's features and explore its vast ecosystem for more advanced use cases.
