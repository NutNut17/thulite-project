---
title: "Docker"
description: ""
summary: ""
date: 2024-10-18T20:27:56+08:00
lastmod: 2024-10-18T20:27:56+08:00
weight: 303
draft: false
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Introduction

#### Docker

{{< inline-svg src="svgs/logos/docker-icon.svg" width="100px" height="79px" class="svg-inline-custom" >}}

Docker is a way to package your app and all its dependencies into a lightweight, portable container that runs consistently across environments.

| Feature | Docker (Containers) | Virtual Machines (VMs) |
| - | - | - |
| Architecture | Runs on the host OS kernel | Includes entire OS (guest OS) |
| Size | Lightweight, typically MBs (shares host OS resources) |Heavyweight, typically GBs (includes OS) |
| Startup Time | Very fast (seconds) | Slower (minutes) |
| Isolation | Process-level isolation, sharing the host kernel | Full OS-level isolation |
| Use Case | Portable apps, microservices, development, CI/CD | Multi-OS support, running legacy apps |

#### Kurbenetes

{{< inline-svg src="svgs/logos/kubernetes.svg" width="100px" height="79px" class="svg-inline-custom" >}}

Kubernetes (often abbreviated as K8s) is an open-source platform for automating the deployment, scaling, and management of containerized applications. It acts as an orchestration tool that manages how containers are deployed, ensures they run smoothly, and automatically handles tasks like scaling and recovery when issues occur.

| Feature | Docker | Kubernetes |
| - | - | - |
| Scope | Manages individual containers | Orchestrates containers at scale |
| Scaling | Manual scaling | Automated scaling |
| Networking | Basic networking | Advanced load balancing and DNS |
| Use Case | Single-host setups | Multi-host, large-scale applications |

#### Deploy Docker on Cloud Infrastructure

General Steps is after building the docker image with dockerfile, push the image to a docker registry and use cloud services that support Docker.

| Cloud Service | Method |
| - | - |
| AWS ECS (Elastic Container Service) | Push image to Amazon Elastic Container Registry (ECR). Create a Task Definition in ECS to use the image. Deploy to an ECS cluster |
| Azure App Service |  Push your image to Azure Container Registry (ACR). Create an Azure App Service to run the container |
| Google Cloud Run | Push your image to Google Container Registry (GCR). Deploy it as a serverless container |
| Heroku or Render | Deploy Docker-based applications directly |
| Kubernetes (GKE, AKS, EKS) | Push your image to a registry. Create Kubernetes manifests (e.g., Deployment, Service). Apply them using `kubectl` |

#### Terminology

| Term | Meaning |
| - | - |
| Images | The blueprints of our application which form the basis of containers. Image are being pushed and pulled. |
| Containers | Created from Docker images and run the actual application |
| Docker Daemon | The background service running on the host that manages building, running and distributing Docker containers. The daemon is the process that runs in the operating system which clients talk to. |
| Docker Client | The command line tool that allows the user to interact with the daemon. More generally, there can be other forms of clients too - such as Kitematic which provide a GUI to the users. |
| Docker Desktop | A desktop app with a GUI to organize dockers. |
| Docker Hub | A remote registry of Docker images ready to be pushed and pulled. |

#### Container Project Structure

```

```

#### Dockerfile

A file to configure how a docker is deployed. In this section, an example project for a full stack deployment on docker will be shown.



To start with docker, initialize a normal repository and add docker related files to build the container.

```Dockerfile
# Build stage
FROM node:alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Serve stage
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
```

This is the content of frontend `Dockerfile`. The `FROM` specifies a base image with node server and using lightweight and multiplatform alpine version. The working directory inside the container will be at `/app`. Then, the local json package file will be copied to the container first to initialize the modules by npm. Then, the rest of local file will be copied to the docker container. Note that the files specified in `.docketignore` will not be copied to the container. After the frontend in container have been built, the container will use ngnix web server of alpine version and and host it on `port 80` of the container.

```Dockerfile
FROM node:alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD [ "npm", "start" ]
```

This is the content of backend `Dockerfile`. It expose port 3000 of the container. Then it runs the `npm start` command defined in `package.json` to start the server inside the container.

```yml
version: '3.8'

services:
  backend:
    build: 
      context: ./backend
    ports:
      - "3000:3000"
    env_file:
      - ./backend/.env

  frontend:
    build: 
      context: ./frontend
    ports:
      - "5173:80"
```

This is a `docker-compose.yml` file, it's the starting point of the docker to run and the image container is defined in `Dockerfile`. In the configuration of the ports, `5173:80` indicates the port 80 in the container is accessible at port 5173 at the host server.

```bash
# Tag might be needed
docker tag docker-test-frontend  nut17/docker-test:frontend   
```

To build and push the image to the repository, run the following code in frontend's terminal. Alpine supports for linux arm64 and amd64 but it cannot work on windows. After the image is built in couple of time, the image will be uploaded to a repository. Do the same for backend. In case of cloud deploy, if the frontend and backend is at different server, the backend api url of frontend had to be adjusted to match.

```bash
docker buildx build --platform linux/amd64,linux/arm64 -t nut17/docker-test:frontend --push .
```

### Docker Commands

#### Lists all images

```bash
docker ps -a:
```

| Information | Description |
| - | - |
| Image id| unique hash identifier |
| Image name | name for image |
| Repository name | The source name of the image in a Docker registry (e.g., Docker Hub). Example: myusername/my-backend-app |
| Tag | A label to differentiate image versions. Example: v1.0, latest. |

#### Online Sharing

You share Docker containers and images online using Docker registries:

```bash
# Push to Docker Hub (or other registries like AWS ECR or Azure Container Registry):
docker login
docker tag your_image username/your_image_name:tag
docker push username/your_image_name:tag

# Pull on another device:
docker pull username/your_image_name:tag
```

The `pull` command fetches the image from the [**Docker registry**](https://hub.docker.com/explore/) and saves it to our system. Image format like `respository/image`, `repository/image:version` format is user defined image and image format like `server:version` is official images.

#### Offline Sharing

```bash
# Save the image to a file:
docker save your_image_name:tag > your_image.tar

# Load the image on the target device:
docker load < your_image.tar
```

#### Run

```bash
docker run <image_name>

# Open terminal for container
docker run -it <image_name> sh

# Show running ports
docker port <image_name>

# Stop container
docker stop <image_name>
```

#### Tag

```bash
```

#### Remove

```bash
docker rm <image_id>
```

#### Multiplatform build and push

```bash
docker buildx build --platform linux/amd64,linux/arm64 -t respository/project:version --push .
```
