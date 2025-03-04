---
title: "API Calls"
description: ""
summary: ""
date: 2024-10-31T17:56:11+08:00
lastmod: 2024-10-31T17:56:11+08:00
draft: false
weight: 109
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### API Calls

In web development, REST (Representational State Transfer) is an architectural style used for designing networked applications. REST APIs (or RESTful APIs) allow different applications to communicate over the web, typically by sending and receiving JSON data. RESTful APIs use standard HTTP methods like GET, POST, PUT, and DELETE to define the actions performed on the data

You will probably need frontend's JavaScript to use API call to an IP address' specific port to make request to a backend server

API creates endpoints specifled by paths `path/to/api/endpoint` and a function is declared at those endpoints in the backend servers. When those api endpoints are reached by frotnend clients, the operation between server and client is made

#### HTTP Methods using Fetch in JS

This is a basic example of fetch

```js
fetch("https://api.example.com/data")
  .then(response => response.json()) // Convert the response to JSON
  .then(data => console.log(data))   // Log the data
  .catch(error => console.error("Error:", error)); // Handle errors
```

This is standard way to do `GET` fetch request

```js
async function fetchData() {
  try {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Error:", error);
  }
}

fetchData();
```

```bash
GET /users?age=30
```

Fetch `POST` request. To send data to the server

```js
fetch("https://api.example.com/user", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({ name: "Alice" })
});
```

Fetch `PUT` request. To update data on server

```js
fetch("https://api.example.com/user/123", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({ name: "Alice Updated" })
});
```

Fetch `DELETE` request. To remove data from server

```js
fetch("https://api.example.com/user/123", {
  method: "DELETE"
});
```

#### HTTP Status Code

- 4XX Client Error
- 5XX Server Error

| Code | Description |
| --- | --- |
| 200 | Successful request, often a GET |
| 201 | Successful request after a create, usually a POST |
| 204 | Successful request with no content returned, usually a PUT or PATCH |
| 301 | Permanently redirect to another endpoint |
| 400 | Bad request (client should modify the request) |
| 401 | Unauthorized, credentials not recognized |
| 403 | Forbidden, credentials accepted but don’t have permission |
| 404 | Not found, the resource does not exist |
| 410 | Gone, the resource previously existed but does not now |
| 429 | Too many requests, used for rate limiting and should include retry headers |
| 500 | Server error, generic and worth looking at other 500-level errors instead |
| 503 | Service unavailable, another where retry headers are useful |

### VS Code Extension: REST Client

You can write a file in VS Code and send this API request to test the functionality

```http {title="example.http"}
POST http://localhost:3001/api/tasks HTTP/1.1
content-type: application/json
{
    "text": "This is a message"
}
```

#### Axios

Axios is a flexible HTTP client for making requests with features like automatic JSON parsing, request/response interception, and easier error handling

```bash
npm install axios
```
```js
import axios from "axios"
try {
  const response = axios.post('https://example.com/api/resource', data, {
    Authorization: `Bearer ${token}`,
  })
  console.log(response.data)
}
catch (error) {
  console.log(error)
}
```

### JWT

JWT (JSON Web Token) is a compact, secure way to transmit information between parties as a JSON object. A server creates token for client, client will keep and use token to verify its identity. Install `jsonwebtoken` package in npm to use.

```js
const jwt = require('jsonwebtoken');
const secretKey = 'your-secret-key';
const user = {
  id: 1,
  username: 'johndoe',
  role: 'admin',
};
// Generate the token
const token = jwt.sign(user, secretKey, { expiresIn: '1h' }); // 1-hour expiry
console.log('Generated Token:', token);

// Middleware to verify JWT
const verifyToken = (req, res, next) => {
  const token = req.headers['authorization']?.split(' ')[1]; // Extract token from "Bearer TOKEN"
  if (!token) return res.status(403).send('Token is required');

  jwt.verify(token, secretKey, (err, decoded) => {
    if (err) return res.status(401).send('Invalid token');
    req.user = decoded; // Attach decoded user data to the request
    next();
  });
};

// Example usage
app.get('/protected', verifyToken, (req, res) => {
  res.send(`Hello, ${req.user.username}! You are authorized.`);
});
```

### HTTPS

HTTPS (HTTP Secure) is an encrypted version of HTTP, using SSL/TLS to secure the data transferred between client and server. Obtaining an SSL Certificate need to purchase from a certificate authority (CA). Certificates usually comes with two files: certificate file `.cf` and private file `.pf`

```js
import express from "express";
import https from "https";
import fs from "fs";

const app = express();

// Read SSL certificate files
const options = {
  key: fs.readFileSync("/path/to/private.key"),
  cert: fs.readFileSync("/path/to/certificate.crt")
};

app.get("/", (req, res) => {
  res.send("Hello, HTTPS world!");
});

// Start HTTPS server
https.createServer(options, app).listen(443, () => {
  console.log("HTTPS server running on port 443");
});
```

Redirect HTTP to HTTPS

```js
const http = require("http");

// Redirect HTTP to HTTPS
http.createServer((req, res) => {
  res.writeHead(301, { Location: `https://${req.headers.host}${req.url}` });
  res.end();
}).listen(80);
```

### API Docs

#### Swagger (OpenAPI)

Swagger is an open-source API documentation tool that generates interactive and downloadable documentation for HTTP APIs. It provides a user-friendly interface for describing and testing APIs. Swagger use JSON or yaml to describe the API endpoints, parameters, and responses.

#### FastAPI

A python framework for building APIs, automatically generates API documentation using swagger UI.

```bash
pip install fastapi uvicorn fastapi[all]
```

```python {title="backend/main.py"}
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

# Enable CORS for frontend requests
app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:5173"],  # Update with frontend URL
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

@app.get("/api/message")
def get_message():
    return {"message": "Hello from FastAPI!"}
```

```bash
uvicorn backend.main:app --reload
```

#### API Implemantation Practice

1. Authentication
2. Authorisation
3. Input validation
4. CRUD
5. Notification (broadcast the event)
6. Output filtering