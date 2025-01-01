---
title: "Production"
description: ""
summary: ""
date: 2024-12-16T18:23:05+08:00
lastmod: 2024-12-16T18:23:05+08:00
draft: false
weight: 111
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Terminology

#### Deployment

Transferring website from developement to a live server. By building the source code into production files. CI/CD automates the deployment process like GitHub Actions.

#### Domain

A website address. DNS (Domain Naming System) maps domain names to the server's IP addres.

#### Hosting

Storing website files on a server so they can be accessed online.

| | Cloud Platform | Web Server |
| - | - | - |
| Description | Third-party hosting provider | Serves on a domain |
| Examples | AWS, Vercel, Netlify | Apache, NGNIX (Engine-X) |

#### Reverse Proxy

A web server like routes requests to appropriate services (e.g., frontend or backend).

#### Web Server

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-6 flex-fill">
          {{< inline-svg src="svgs/logos/apache.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-6 flex-fill">
          {{< inline-svg src="svgs/logos/nginx.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

Web server handle HTTP requests, serve content, and manage traffic for web applications. Think web servers as a vanilla server that serve website. Ngnix is newer than Apache and are more modern.

| Technology | Examples | Interaction with web server |
| - | - | - |
| Application Server | Node.js | Have overlapped functionality but node is not web server |
| Developement Tool | Vite, Nuxt, Next | After the dev tool built static site, web server hosts the static sites (proxy) |
| Cloud Platform | AWS, Azure | Offer managed solutions that reduce the need for direct Apache/NGINX use in many scenarios |
| OS | Linux | Foundation for web server deployment |

#### VPS (Virtual Private Server)

{{< inline-svg src="svgs/logos/digitalocean.svg" width="100px" height="79px" class="svg-inline-custom" >}}

![digitalocean](/svgs/logos/digitalocean.png)

A VPS is a virtual machine offered by hosting providers, giving you control over a portion of a physical server. It's like having your own private server without sharing resources with other users. Some popular VPS provider: DigitalOcean, Linode, Vultr, AWS Lightsail

#### Full-Stack Deployment

Hosting both frontend and backend together on a single or integrated platform.

#### Serverless

A hosting model where the cloud provider manages the server infrastructure for you (e.g., AWS Lambda, Vercel Functions).

#### CDN (Content Delivery Network)

A global network of servers that deliver static content quickly to users (e.g., Cloudflare, AWS CloudFront).

### Platforms

#### Azure vs AWS vs Firebase

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/azure.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/firebase.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/aws.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

| | Microsoft Azure | Amazon AWS | Google Firebase |
| - | - | - | - |
| Ease of Use | Moderate | Advanced | Beginner-friendly |
| Static Hosting | Static Web Apps (CI/CD with GitHub, Azure DevOps), Azure Blob Storage | S3 + Cloud Front(For fast flobal delivery) | Firebase Hosting |
| Dynamic Hosting | App Service, Azure Kubernetes Service (AKS), VMs | EC2, Beanstalk, Lambda | Firebase Cloud Functions |
| Serverless | Azure Functions | AWS Lambda | Firebase Cloud Functions |
| Pricing | Pay-as-you-go, predictable | Highly scalable, variable | Free tier for small projects |
| Best for | Enterprises, static sites with serverless APIs, dynamic apps with scalability | Businesses needing scalability and advanced customization | Startups and small to medium projects needing a fast, integrated backend + frontend setup |

#### Cloud Platforms for Frontend

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/netlify.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/vercel.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/firebasehosting.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
    <div class="row">
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/githubpages.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/aws-s3.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/cloudfront.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

These platform only can do dynamic hosting and lightweight backend using serverless function

| Platform | Static | Dynamic | Feature |
| - | - | - | - |
| Netlify | O | O | Great for SPAs and static websites |
| Vercel | O | O | Ideal for static or SSR-enabled apps |
| Firebase Hosting | O | O | Excellent for SPAs, especially with Firebase integrations |
| GitHub Pages | O | X | - |
| AWS S3 + Cloud Front | O | X | Great for hosting static websites or SPAs |

#### Cloud Platforms for Backend

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/heroku.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/render.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/ec2.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
    <div class="row">
        <div class=" col-12 col-sm-6 flex-fill">
          {{< inline-svg src="svgs/logos/elasticbeanstalk.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-6 flex-fill">
          {{< inline-svg src="svgs/logos/lambda.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

These framework support full backend frameworks

| Platform | Static | Dynamic | Feature |
| - | - | - | - |
| Heroku | X | O | Suitable for frontend + backend hosting together in one app |
| Render | O | O | Ideal for dynamic backends or full-stack apps |
| AWS EC2 + Elastic Beanstack (For deploying dynamic apps) + Lambda | O | O | Excellent for dynamic backends |

Todo: Developement HTTPS, Deployment
