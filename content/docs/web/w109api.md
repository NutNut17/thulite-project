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

### VS Code Extension: REST Client

You can write a file in VS Code and send this API request to test the functionality

```http {title="example.http"}
POST http://localhost:3001/api/tasks HTTP/1.1
content-type: application/json
{
    "text": "This is a message"
}
```

### Axios

Axios is a flexible HTTP client for making requests with features like automatic JSON parsing, request/response interception, and easier error handling

### HTTPS

HTTPS (HTTP Secure) is an encrypted version of HTTP, using SSL/TLS to secure the data transferred between client and server. Obtaining an SSL Certificate need to purchase from a certificate authority (CA)

CErtificates usually comes with two files: certificat file `.cf` and private file `.pf`

Implementation on Express.js

```js
const express = require("express");
const https = require("https");
const fs = require("fs");

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