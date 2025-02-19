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
my-docker-project/
│-- backend/
│   ├-- Dockerfile
│   ├-- package.json
│   ├-- server.js
│   ├-- src/
│   └-- node_modules/
│
│-- frontend/
│   ├-- Dockerfile
│   ├-- package.json
│   ├-- vue.config.js
│   ├-- src/
│   └-- node_modules/
│
│-- db-data/                  # Persistent database volume (bind mount)
│
│-- nginx/
│   ├-- default.conf           # Nginx configuration for reverse proxy
│   └-- Dockerfile
│
│-- docker-compose.yml
│-- .env                       # Environment variables
│-- .gitignore
│-- README.md

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

This is the content of frontend `Dockerfile`. The `FROM` specifies a base image with node server and using lightweight and multiplatform alpine version. The working directory inside the container will be at `/app`. Then, the local json package file will be copied to the container first to initialize the modules by npm. Then, the rest of local file will be copied to the docker container. Note that the files specified in `.dockerignore` will not be copied to the container. After the frontend in container have been built, the container will use ngnix web server of alpine version and and host it on `port 80` of the container.

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

#### Multiplatform build and push

Use `buildx` for advanced build like multiplatform build, caching, remote build, CI/CD integration.

```bash
# Tag first
docker tag docker-test-frontend nut17/docker-test:frontend 
docker buildx build --platform linux/amd64,linux/arm64 -t nut17/docker-test:frontend --push .
```

To build and push the image to the repository, run the following code in frontend's terminal. Alpine supports for linux arm64 and amd64 but it cannot work on windows. After the image is built in couple of time, the image will be uploaded to a repository. Do the same for backend. In case of cloud deploy, if the frontend and backend is at different server, the backend api url of frontend had to be adjusted to match.

### Docker Commands

#### Lists all images

```bash
docker ps -a
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

The `pull` command fetches the image from the [Docker registry](https://hub.docker.com/explore/) and saves it to our system. Image format like `respository/image`, `repository/image:version` format is user defined image and image format like `server:version` is official images.

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

A tagged image can tell more information about the version of the image

```bash
docker tag my-app-image-id my-app:1.0.0 # Tag an image
docker build -t my-app:1.0.0 .          # Tag while building an image
docker push my-dockerhub-username/my-app:1.0.0 # Push tagged image to a registry
```

#### Remove

```bash
docker rm <image_id>
```

### Advanced Concepts

#### Docker Network

A container have it's own IP address and in default, they share over the default network bridge. We can isolate some containers into a private network.

```bash
#!/bin/bash

# build the flask container
docker build -t yourusername/foodtrucks-web .

# create the network
docker network create foodtrucks-net

# start the ES container
docker run -d --name es --net foodtrucks-net -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:6.3.2

# start the flask app container
docker run -d --net foodtrucks-net -p 5000:5000 --name foodtrucks-web yourusername/foodtrucks-web

# Remove network
docker network rm network_name

# Inspect network
docker network inspect network_name
```

- `-d`: Runs the container in detached mode (background).
- `-p 9200:9200 -p 9300:9300`: 9200 is the main REST API port for Elasticsearch, 9300 is the internal port used for inter-node communication in Elasticsearch clusters.
- `-e "discovery.type=single-node"`: Sets an environment variable inside the container, configures Elasticsearch to run in "single-node" mode, bypassing clustering logic. This is commonly used for development or testing environments.

#### Docker Compose

A tool for defining and running multi-container Docker applications.

```yml
version: "3"
services:
  es:
    image: docker.elastic.co/elasticsearch/elasticsearch:6.3.2
    container_name: es
    environment:
      - discovery.type=single-node
    ports:
      - 9201:9200
    volumes:
      - esdata1:/usr/share/elasticsearch/data
  web:
    build: .
    command: python3 app.py
    environment:
      - DEBUG=True
    depends_on:
      - es
    ports:
      - 5000:5000
    volumes:
      - ./flask-app:/opt/flask-app
volumes:
  esdata1:
    driver: local
```

This is a `docker-compose.yml` file, it's the starting point of the docker to run and the image container is defined in `Dockerfile`.

- `9200:9200` indicates the port 9201 in the container is accessible at port 9200 at the host server.
- `build`: Docker will look for a Dockerfile in the current directory to build the image in developement. Follow `image` configurations in the es container for release.
- `environment: - DEBUG=True`: tells flask to update the server by changes in project.
- `depends_on` tells docker to start the es container before web container.
- `volumes` mount points in container for persistent database after restart.

```bash
# Run
docker-compose up

# Stop containers
docker-compose down 

# Stop and remove named volume
docker-compose down -v
```

#### Persistent Data

Docker provides two main ways to manage persistent data: Named Volumes and Bind Mounts. 

A named volume is managed entirely by Docker, and Docker decides where to store it on the host machine. This is more portable but harder to access directly from host.

```yml
services:
  myapp:
    image: myimage
    volumes:
      - mydata:/app/data
```
- `mydata`: Named volume managed by Docker.
- `/app/data`: Path inside the container where the volume is mounted.

A bind mount directly links a specific directory on the host machine to a directory inside the container. This provides real-time synchronization of files between the host and the container. Better for code sharing during developement

```yml
services:
  web:
    image: myimage
    volumes:
      - ./my-local-dir:/app/data
```
- `./my-local-dir`: Path on the host machine (relative to the compose file).
- `/app/data` : Path inside the container where the folder is mounted. 

Reference: [Docker Curriculum](https://docker-curriculum.com/)