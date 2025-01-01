---
title: "Express.js"
description: ""
summary: ""
date: 2024-10-31T18:23:05+08:00
lastmod: 2024-10-31T18:23:05+08:00
draft: false
weight: 110
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

{{< inline-svg src="svgs/logos/express.svg" width="100px" height="79px" class="svg-inline-custom" >}}

### Setting Up

Express.js is a simplified Node.js framework to create a web server. A seperated server of web server and database server is served at different port

```bash
# Initialize a Node.js project
npm init -y
npm install express
```

Run the express server using this command

```bash
node server.js
```

{{< link-card
  title="Vue + Express Fullstack Web Example"
  description="A reference to setup a fullstack frontend and backend using Vue and Express.js"
  href="https://mertgursoy.medium.com/how-to-create-a-basic-to-do-crud-app-using-vue3-nodejs-expressjs-server-sqlite-vite-03a29509ada4"
  target="_blank"
>}}

### Web Server

```js {title="server.js"}
const express = require('express');
const cors = require('cors');
const path = require('path');

const app = express();
const PORT = 3000;

// Enable CORS for all routes
app.use(cors());

// Define a route
app.get('/', (req, res) => {
res.send('Hello from Express.js!');
});

// Serve static files from the "public/images" folder
app.use('/images', express.static(path.join(__dirname, 'public/images')));

// Start the server
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```

```js {title="server.mjs"}
// Able to configure package.json to use es module using .js file too

import express from 'express';
import cors from 'cors';
import path from 'path';
import { fileURLToPath } from 'url';

const app = express();
const PORT = 3000;

// Enable CORS
app.use(cors());

// Resolve the directory name (required for .mjs files)
const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

// Serve static files from the "public" folder
app.use('/images', express.static(path.join(__dirname, 'public/images')));

// Start the server
app.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}`);
});

```

#### CORS

CORS (Cross-Origin Resource Sharing) is a security feature built into web browsers that controls how resources (like APIs, fonts, images, etc.) on a web server can be accessed from a different domain than the server itself. It helps prevent malicious sites from accessing sensitive data on other sites without permission.

To enable CORS, add this code to Express server

```js
app.use(cors({
  origin: "https://frontend.com",
  methods: ["GET", "POST"],
  allowedHeaders: ["Content-Type", "Authorization"]
}));
```

### Database Server

A seperated server for database is required

#### SQLite

In this example, we will demostrate setting up a SQLite database server. But first, some required package need to be installed

Sequelize is a modern TypeScript and Node.js ORM for Oracle, Postgres, MySQL, MariaDB, SQLite and SQL Server, and more. ORM stands for Object-Relational Mapping, which is a software tool that connects programming code with database structures

```bash
npm install sequelize
npm install sqlite3
```

```js
// Set up Sequelize to use SQLite
const { Sequelize, DataTypes } = require('sequelize');
const sequelize = new Sequelize ({
    dialect: 'sqlite',
    storage: './database.sqlite'
})
var db = {}


// Define task model to make operation on SQLite using sequelize
async function setupDB() {
    try {
        db.Task = sequelize.define('Task', {
            text: {
                type: DataTypes.STRING,
                allowNull: false
            },
        });
        // Database initialization
        await sequelize.sync({ force: true });
        await db.Task.create({ text: "Item-1-MertKadirGursoy"});
        await db.Task.create({ text: "Item-2"});
        await db.Task.create({ text: "Item-3"});
    } catch (error) {
        console.error(error);
    }
}

// CREATE APIs URL ENDPOINTS TO CREATE AND DELETE TO DO ITEMS
async function startServer() {
    try {
        await setupDB()
        const port = 3001
        const express = require('express')
        const cors = require('cors')
        const app = express()
        app.use(express.json())

        // Define api endpoints

        // GET METHOD API URL | TESTING
        app.get('/', (req, res) => {
            res.send('hello world')
        })
        // GET METHOD API URL | RETRIEVE ITEMS
        app.get('/api/tasks', (req, res) => {
            // return all taskls
            db.Task.findAll().then(tasks => {
                res.json(tasks)
            })
        })
        // POST METHOD API URL | CREATE ITEM
        app.post('/api/tasks', (req, res) => {
            // create a task
            db.Task.create(req.body)
                .then(task => {
                    res.status(201).json(task); // Send the created task back with a 201 status
                })
                .catch(error => {
                    console.error('Error creating task:', error);
                    res.status(400).json({ error: 'Failed to create task' }); // Handle validation errors
        });
        })
        // DELETE METHOD API URL | DELETE ITEM
        app.delete('/api/tasks/:id', (req, res) => {
            // delete a task
            db.Task.destroy({
                where: {
                    id: req.params.id
                }
            }).then(() => {
                res.sendStatus(204);
            }).catch((error) => {
                console.error(error);
                res.sendStatus(500); // Internal Server Error
            });
        });

        // Activate API
        app.listen(port, () => {
            console.log(`App listening on port ${port}`)
        })
    } catch (error) {
        console.error(error);
    }
}
startServer()
```

Then, calling the HTTP request below should add a new data to the database

```js
POST http://localhost:3001/api/tasks HTTP/1.1
content-type: application/json
{
    "text": "Item-4"
}
```

{{< callout context="note" title="Note" icon="outline/info-circle" >}}
Use SQLite Viewer extension on VS Code to view the database
{{< /callout >}}
