---
title: "Docker Basics"
written by: "Rohit Singh Bhandari"
date: 2024-02-07T17:15:22+05:30
draft: false
---

## Introduction:<br>

In recent years, Docker has revolutionized the way software is developed, deployed, and managed. Its impact on the software industry is profound, offering a streamlined approach to building, shipping, and running applications. In this guide, we will explore what Docker is, why it is important, and delve into its key features and functionalities.

## What is Docker?<br>

Docker is an open-source platform that enables developers to package their applications and dependencies into lightweight, portable containers. These containers are isolated environments that contain everything needed to run the application, including code, runtime, system tools, and libraries. Unlike virtual machines, Docker containers share the host system's kernel and are more efficient in terms of resource utilization and performance.

## Early Days: Before Docker<br>

Prior to Docker, deploying and managing applications in production environments was a complex and time-consuming process. Developers had to deal with compatibility issues, dependency conflicts, and differences between development and production environments. Virtual machines offered one solution to these challenges but came with overhead in terms of resource consumption and performance.

Traditionally, for each application, a new server was provisioned, leading to increased hardware requirements and costs. This approach was not scalable and resulted in inefficient resource utilization.

Docker changed this paradigm by introducing a more lightweight and efficient alternative. By encapsulating applications and their dependencies into containers, Docker eliminated many of the hurdles associated with traditional deployment methods.

## Mid Scenario:

VMware introduced virtualization, allowing multiple applications to run on a single physical server. Virtual machines (VMs) provided isolation but required dedicated resources, including storage, CPU, and RAM. Dependency issues arose when sharing projects between environments due to differences in configurations.

## Key Concepts and Features:<br>

* Images: Docker images are read-only templates that contain the application code, runtime, libraries, and other dependencies. Images serve as the basis for creating Docker containers.

* Containers: Docker containers are lightweight, portable, and self-sufficient runtime environments that encapsulate applications and their dependencies. Containers can be run, started, stopped, and deleted using Docker commands.

* Dockerfile: A Dockerfile is a text document that contains instructions for building a Docker image. It specifies the base image, environment variables, dependencies, and commands needed to set up the application environment. Dockerfile is used to define the instructions for building Docker images.
    
    Images can be built using(Navigate to the directory containing your Dockerfile)
    
     Build the Docker image
    `docker build -t your-image-name .`

     Push the image to Docker Hub
    `docker push dockerhub_username/image_name`

     Tag the image before pushing (if needed)
    `docker tag image_name dockerhub_username/image_name`

     Log in to Docker Hub
    `docker login`

     Run the Docker container from the image
    `docker run -p 9090:8080 your-image-name`

* Docker Compose: Docker Compose is a tool for defining and running multi-container Docker applications. It uses a YAML file to define services, networks, and volumes, making it easy to manage complex applications with multiple components.

## Some useful docker commands

List all Docker containers (including stopped ones)<br>
`docker ps -a`

List only running Docker containers<br>
`docker ps`

List all Docker images<br>
`docker images`

List only the IDs of Docker images<br>
`docker images -q`

Start a stopped container<br>
`docker start container_id`

Stop a running container<br>
`docker stop container_id`

Commit changes in a Docker container to create a new image<br>
`docker commit -m "added something" container_id your_image_name`

Delete non-running containers<br>
`docker container prune`

## Demo Spring Boot application using Docker

**Dockerfile Creation and Image Building**

```
# Define the base image with Java 17
FROM openjdk:17

# Expose port 8080 for the Spring Boot application
EXPOSE 8080

# Add the compiled JAR file of your Spring Boot application to the container
ADD target/your-application.jar your-application.jar

# Specify the command to run the Spring Boot application when the container starts
ENTRYPOINT ["java", "-jar", "/your-application.jar"]
```
**Building the Docker Image**<br>
Navigate to the root directory of your Spring Boot project where the Dockerfile is locatedand use the docker build command to build the Docker image, providing a tag name for the image.
`docker build -t your-image-name .`

**Running the Docker Container**<br>
Once the Docker image is built, you can run a Docker container based on that image.
`docker run -p 9090:8080 your-image-name`
`-p 9090:8080` maps port 8080 inside the Docker container to port 9090 on the host machine. This mapping allows you to access the Spring Boot application by connecting to port 9090 on your host machine.

## Conclusion:<br>
In conclusion, Docker has revolutionized the way software is developed, deployed, and managed. Its lightweight, portable containers provide a consistent environment across different platforms, enabling developers to build and deploy applications with ease. By understanding the fundamentals of Docker and its key features, developers can streamline their workflows and improve the efficiency of their software development lifecycle. Embracing Docker is not just a trend but a necessity in today's fast-paced world of software development.
Overall it was the basic understanding of docker, rest we will add more blogs as we'll proceed.