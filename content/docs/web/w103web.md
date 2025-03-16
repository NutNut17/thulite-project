---
title: "Web Tech Stack"
description: ""
summary: ""
date: 2024-10-10T16:43:10+08:00
lastmod: 2024-10-10T16:43:10+08:00
draft: false
weight: 103
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---
### Web Structure

Modern website uses HTML (HyperText Markup Language) to define the structure of webpage, CSS (Cascading Style Sheets) used to style and layout HTML elements. JS (JavaScript) allows you to make a webpage interaction.

<div class="container-fluid"  style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/html-5.svg" width="192px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/css-3.svg" width="192px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/javascript.svg" width="192px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

{{< tabs "website" >}}
{{< tab "example.html" >}}

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Website Title</title>
    <style> /* CSS styles for this file */</style>
    <link rel="stylesheet" href="example.css"> <!-- External CSS link -->
</head>
<body>
    <h1>This is a Header</h1>
    <p>This is a paragraph. Html are made of element with tags, they may have some attribute declared inside the tags<>. id attribute is used to uniquely give an id to an elements, while class attribute is used to groups elements. </p>

    <button id="button1" class="buttonClass" >Click Me!</button>

    <script></script> <!-- Internal JS script -->
    <script src="example.js"></script> <!-- External JS link -->
</body>
</html>
```

However, coding from scratch is less effective. But there is lots of framework with many functionalies and feature to be introduced in this site

{{< /tab >}}
{{< tab "example.css" >}}

```css
body {
    font-family: Arial, sans-serif;
}
h1 {
    color: green;
}
#button1 {
  color: gray;
}
.buttonClass {
  background-color: green;
}
```

{{< /tab >}}
{{< tab "example.js" >}}

```js
// Declaring variables
var x = 5;        // Global or function-scoped
let y = 10;       // Block-scoped (good practice)
const z = 15;     // Constant value, cannot be changed

// Function declaration
function sayHello(name) {
    console.log("Hello " + name + "!");
    return true;
}
sayHello("User");

// Anonymous Function
let multiply = function(a, b) { return a * b; };
console.log(multiply(5, 3)); // Outputs: 15

// Arrow Function
let divide = (a, b) => a / b;
console.log(divide(10, 2)); // Outputs: 5


```

{{< link-card
  title="JavaScript"
  description="Click here to understand basics of JavaScript"
  href="/docs/web/javascript/"
>}}

{{< /tab >}}

{{< /tabs >}}

### CSS Frameworks

Some tools to enhance the quality and productivity of CSS

#### Bootstrap

<div style="margin: 1.5rem"> </div>

![Bootstrap](svgs/logos/bootstrap.png)

<div style="margin: 1.5rem"> </div>

A simple and quick developement CSS framework for easy designing by adding predefined bootstrap class such as buttons, styles, layout on the html element class attribute. Visit [Bootstrap](https://getbootstrap.com/docs/5.3/getting-started/introduction/) website for more info and customization. Add the following source in html to start using bootstrap.

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
```

#### SASS & SCSS

<div style="margin: 3rem">
  {{< inline-svg src="svgs/logos/sass.svg" width="192px" height="150px" class="svg-inline-custom" >}}
</div>

SASS (Syntactically Auwsome Style Sheets) is a CSS extension to add more functionality to CSS, and needs to compile to CSS. SASS have similar syntax to python. While SCSS (Sassy SASS) is a syntax of SASS similar to Java. The key feature are variables, nesting, mixins (bundle some properties), inheritance, mathematics operations and partials (multiple files). Below are the example page and code.

{{< details "Show Demo" >}}

<iframe src="/scss" width="100%" height="300" style="border:none;"></iframe>

{{< tabs "sass">}}
{{< tab "index.html" >}}

```html
<!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>SCSS and Sass Example</title>
      <link rel="stylesheet" href="styles.css">
  </head>
  <body>
      <div class="container">
          <header class="header">
              <h1>Demo</h1>
          </header>
          <div class="content">
              <p>This is a demo for SCSS and Sass features.</p>
              <button class="button">Primary Button</button>
              <button class="secondary-btn">Secondary Button</button>
          </div>
          <footer class="footer">
              <p>&copy; 2024 Nut17</p>
          </footer>
      </div>
  </body>
  </html>
```

{{< /tab >}}
{{< tab "styles.css" >}}

```css

/* Generated CSS */
.button, .secondary-btn {
  padding: 10px 20px;
  background-color: #3498db;
  color: white;
  border-radius: 5px;
  text-transform: uppercase;
}
.button:hover, .secondary-btn:hover {
  background-color: #217dbb;
}

.secondary-btn {
  background-color: #2ecc71;
}
.secondary-btn:hover {
  background-color: #25a25a;
}

.button, .secondary-btn {
  padding: 10px 20px;
  background-color: #3498db;
  color: white;
  border-radius: 5px;
  text-transform: uppercase;
}
.button:hover, .secondary-btn:hover {
  background-color: #217dbb;
}

.secondary-btn {
  background-color: #2ecc71;
}
.secondary-btn:hover {
  background-color: #25a25a;
}

body {
  font-family: Helvetica, sans-serif;
  background-color: #e1f0fa;
  margin: 0;
  height: 100vh; /* Make sure the body takes the full height of the viewport */
  display: flex;
  justify-content: center;
  align-items: center;
}/*# sourceMappingURL=styles.css.map */
```

{{< /tab >}}
{{< tab "SCSS" >}}

```css
/* From styles.scss */
@import 'variables';  /* From _variables.scss */
@import 'mixins';     /* From _mixins.scss */
@import 'buttons';    /* From _buttons_.scss */
@import 'layout';     /* From _layout_.scss */

body {
  font-family: $font-stack;
  background-color: lighten($primary-color, 40%);
  margin: 0;
  height: 100vh; /* Make sure the body takes the full height of the viewport */

  @include flex-center;
}

/* From _variables.scss  */

$primary-color: #3498db;
$secondary-color: #2ecc71;
$font-stack: Helvetica, sans-serif;
$base-padding: 10px;

/* From _mixins.scss */

@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
  -moz-border-radius: $radius;
  border-radius: $radius;
}

/* From _buttons_.scss */

.button {
  padding: $base-padding 20px;
  background-color: $primary-color;
  color: white;
  @include border-radius(5px);
  text-transform: uppercase;

  &:hover {
    background-color: darken($primary-color, 10%);
  }
}

.secondary-btn {
  @extend .button;
  background-color: $secondary-color;

  &:hover {
    background-color: darken($secondary-color, 10%);
  }
}

/* From _layout_.scss */

.button {
  padding: $base-padding 20px;
  background-color: $primary-color;
  color: white;
  @include border-radius(5px);
  text-transform: uppercase;

  &:hover {
    background-color: darken($primary-color, 10%);
  }
}

.secondary-btn {
  @extend .button;
  background-color: $secondary-color;

  &:hover {
    background-color: darken($secondary-color, 10%);
  }
}

```

{{< /tab >}}
{{< tab "SASS" >}}

```sass
/* From styles.sass */

@import variables
@import mixins
@import buttons
@import layout

body
  font-family: $font-stack
  background-color: lighten($primary-color, 40%)
  margin: 0


/* From _variables.sass */

$primary-color: #3498db
$secondary-color: #2ecc71
$font-stack: Helvetica, sans-serif
$base-padding: 10px

/* From _mixins.sass */

=flex-center
  display: flex
  justify-content: center
  align-items: center

=border-radius($radius)
  -webkit-border-radius: $radius
  -moz-border-radius: $radius
  border-radius: $radius

/* From _buttons_.sass */

.button
  padding: $base-padding 20px
  background-color: $primary-color
  color: white
  +border-radius(5px)
  text-transform: uppercase

  &:hover
    background-color: darken($primary-color, 10%)

.secondary-btn
  @extend .button
  background-color: $secondary-color

  &:hover
    background-color: darken($secondary-color, 10%)

/* From _layout_.sass */

.container
  width: 100%
  padding: $base-padding

  .header
    +flex-center
    height: 100px
    background-color: $primary-color
    color: white

  .content
    display: flex
    flex-direction: column
    padding: $base-padding * 2

  .footer
    height: 50px
    text-align: center
    background-color: $secondary-color
    padding: $base-padding

```

{{< /tab >}}
{{< /tabs >}}

{{< /details >}}

#### Tailwind CSS

<div style="margin: 3rem">
{{< inline-svg src="svgs/logos/tailwindcss-icon.svg" width="192px" height="150px" class="svg-inline-custom" >}}
</div>

A optimized and lightweight CSS framework with highly customizable developement and more configuration space than Bootstrap. Tailwind CSS does not impose a predefined style for components, but they have a utilities class to help building components. Tailwind also have 'purge' feature to remove unused CSS. Visit [Tailwind CSS](https://tailwindcss.com/) website for more info.

#### Purge CSS

<div style="margin: 3rem">
{{< inline-svg src="svgs/logos/purgecss.svg" width="192px" height="150px" class="svg-inline-custom" >}}
</div>

A tool to remove unused CSS. Visit [PurgeCSS](https://purgecss.com/) to learn how to use. Build tools like PostCSS or TailwindCSS can configure and automate the purging of CSS.

```bash
npm install -g purgecss
purgecss --css styles.css --content index.html --output purified.css
```

#### Font

Fonts-families tell what font type to be used. Font-weight defind the thickness of the font. Font-styles are like italic, underline, etc.

| Font Family | Characteristics |
| --- | --- |
| Serif | Classic, traditional official fonts |
| Sans-serif | Modern, simple fonts |
| Monospace | Every character have same width |
| Cursive | Cursive writing |

Scaling of fonts

| Unit | Description | Example |
| - | - | - |
| Pixel | The absolute pixel size| 16px |
| Em | Relative unit based on parent element| 1.5em |
| Rem | Relative to root element| 1.5 rem |
| Percentage | Relative to the parent element| 50% |
| Viewport | 1 unit is the 1% of the browser's visible window | 3vw(width); 4vh(height) |
| Points | 1 points is 1/72 inch used in traditional printing media| 12pt |

The font size represent the height of the character from the top to the bottom of the part. IT industry uses combination of `rem` for consistenst typography across pages and `vw` for large dynamix text that adapt screen size. Default of html font size is 16px

Below shows an example using Google Fonts

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Google Fonts Example</title>
    <!-- Link to Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&family=Lobster&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
        }
        h1 {
            font-family: 'Lobster', cursive; /* Use Lobster font */
            font-size: 48px;
        }
    </style>
</head>
<body>
    <h1>Welcome to My Website!</h1>
    <p>The title uses Lobster font while paragraph uses Roboto font </p>
</body>
</html>

```

#### Icons

Discover amazing icon from [FontAwesome](https://fontawesome.com/start) and embed into web.

```html {title="fontawesome-example.html"}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Font Awesome with Custom Styles</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        .icon {
            margin: 15px;
        }
        /* Custom styles for different icons */
        .fa-home {
            color: #4CAF50; /* Green */
            font-size: 2em;
        }
    </style>
</head>
<body>
    <i class="fas fa-home icon"></i>    <!-- Home icon with custom styles -->
</body>
</html>
```

#### Figma

<div style="margin: 3rem">
{{< inline-svg src="svgs/logos/figma.svg" width="192px" height="100px" class="svg-inline-custom" >}}
</div>

Figma is a web application for interface design. Making layout with autolayout, variable. However, the website need to be coded manually by looking at the design information. Learn more about it [here](https://youtu.be/1pW_sk-2y40?si=oNPkjwPuT6XGl4Qr)

For quick web UI/UX design tutorial, watch [this](https://youtu.be/wIuVvCuiJhU?si=sHtVr2IlgOZc7g_B). For color testing, visit this [website](https://www.realtimecolors.com/?colors=050315-fbfbfe-2f27ce-dedcff-433bff&fonts=Inter-Inter) from Juxtopposed to test with color selection.

Try to implement these design: minimal, glass morphic, neobrutalist, grainy, modern

### Frontend Frameworks

Frontend Frameworks provide better way to make website efficiently, dynamically, and consistent.

| Static Site | Dynamic Site |
| - | - |
| Website consisting only HTML, CSS, JS | Interacts with backend |

#### React vs Vue (Dynamic)

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-6 flex-fill">
          {{< inline-svg src="svgs/logos/react.svg" width="192px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-6 flex-fill">
          {{< inline-svg src="svgs/logos/vue.svg" width="192px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

React is a JS library for building UI. React focusing on virtual DOM efficient rendering, and uses state (internal component data) and props (data passed to components) for dynamic data. It is suitable for creating complex web application.

Vue is an open-source JS framework for building single-page application similar to Angular. Vue uses reactivity system that change in data is automatically reflected to UI. Templates is available to bind DOM to Vue instance data.

| Features | React | Vue |
| - | - | - | - |
| Learning Curve | Steep | Gentle |
| Performance | Great on large, complex project | Great on small-medium, simple project |
| State Management | Using hooks (Redux, Zustand) | Using reactive data (Pinia) |
| Data Binding | One-way data binding (parent to child) | Two-way data binding |
| Community | Vast and mass support and supported by Facebook | Growing Rapidly |

{{< link-card
  title="Vue"
  description="Click here to explore more about Vue"
  href="/docs/web/vue/"
>}}

#### Hugo (Static)

<div style="margin: 3rem">
{{< inline-svg src="svgs/logos/hugo.svg" width="192px" height="79px" class="svg-inline-custom" >}}
</div>

A framework wrtitten on GO for static content. It's very quick to build up. This website is powered by Hugo.

### Backend Tools

#### Typescript

<div style="margin: 3rem">
{{< inline-svg src="svgs/logos/typescript-icon.svg" width="192px" height="79px" class="svg-inline-custom" >}}
</div>

A language derived from javascript to deal with variable type consistency and adds Java programming features like OOP, generics, enum, union and intersection types. Typescript can be compiled to javascript. Tyepscript is suitable for developing and debugging huge JS projects. Visit [Typescript](https://www.typescriptlang.org/) website to learn more.

{{< details "Typescript Code" >}}

```typescript
// TypeScript Example: Person and Employee Management

// Define a type alias for a string or number
type ID = string | number;

// Interface for an Employee
interface Employee {
  id: ID;
  name: string;
  age: number;
  position: string;
  displayInfo(): string;
}

// Class for a Person
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): string {
    return `Hello, my name is ${this.name}, and I am ${this.age} years old.`;
  }
}

// Class Employee that extends Person and implements Employee interface
class FullTimeEmployee extends Person implements Employee {
  id: ID;
  position: string;

  constructor(id: ID, name: string, age: number, position: string) {
    super(name, age);
    this.id = id;
    this.position = position;
  }

  // Implementation of displayInfo method from Employee interface
  displayInfo(): string {
    return `Employee ID: ${this.id}, Name: ${this.name}, Position: ${this.position}`;
  }
}

// Function to print a person's greeting
function printGreeting(person: Person): void {
  console.log(person.greet());
}

// Create an instance of FullTimeEmployee
const employee: FullTimeEmployee = new FullTimeEmployee(101, "John Doe", 28, "Software Engineer");

// Use the methods
printGreeting(employee); // Output: Hello, my name is John Doe, and I am 28 years old.
console.log(employee.displayInfo()); // Output: Employee ID: 101, Name: John Doe, Position: Software Engineer

```

{{< /details >}}

#### Eslint

<div style="margin: 3rem">
{{< inline-svg src="svgs/logos/eslint.svg" width="192px" height="79px" class="svg-inline-custom" >}}
</div>

A tool to identifying and fixing common issue in JavaScript on syntax error, potential bugs and code style

#### Wordpress

<div style="margin: 3rem">
{{< inline-svg src="svgs/logos/wordpress-icon.svg" width="192px" height="79px" class="svg-inline-custom" >}}
</div>

A full-stack online web content management system. Build website with templates easily

### Backend Framework

| Server-Side Rendering | Client-Side Rendering |
| - | - |
| HTML generated at server | HTML generated at client |
| Faster initial load, better SEO (Search Engine Optimization) | Slower initial, faster transition between pages |
| Suitable for content-heavy website, SEO-cricital apps | Highly interactive, dynamic apps |

| | Static Site | Dynamic Site |
| - | - | - |
| Description | A website consisting only of HTML, CSS, and JavaScript files with no backend | A website that interacts with a backend for features like APIs or databases |
| Hosting Platform | Netlify, Vercel, GitHub Pages, Firebase Hosting, AWS S3 + Cloud Front | Netlify, Vercel, Heroku, Render, AWS (EC2, Elastic Beanstack, Lambda) |
| Frameworks | React(Vite), Vue(Vite), Next.js, Nuxt.js, Hugo | Vue, React, Angular, Svelte, Node.js, Python, PHP Laravel, Ruby on Rails |

A backend web server is used to manage client request (Apache or Ngnix). Visit production to learn more on how to make website available to public.

{{< link-card
  title="Production"
  description="Click here to learn more about hosting platform"
  href="/docs/web/production/"
>}}

#### Nuxt.js vs Next.js

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-6 flex-fill">
          {{< inline-svg src="svgs/logos/nuxt.svg" width="192px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-6 flex-fill">
          {{< inline-svg src="svgs/logos/nextjs.svg" width="192px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

| Features | Nuxt | Next |
| - | - | - |
| Parent Framework | Vue | React |
| Render | Server-side render | Server-side render |
| Generation | Static | Static |
| Dev tool | Routing, state management | Routing, state management |

#### Vite

<div style="margin: 3rem">
{{< inline-svg src="svgs/logos/vite.svg" width="192px" height="79px" class="svg-inline-custom" >}}
</div>

A fast, modern build tool and development server for JavaScript and TypeScript projects. It focuses on lightning-fast cold starts and efficient bundling for production. [Vite website](https://vite.dev/)

#### Node.js

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-6 flex-fill">
          {{< inline-svg src="svgs/logos/nodejs.svg" width="192px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-6 flex-fill">
          {{< inline-svg src="svgs/logos/nodejs-icon.svg" width="192px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

Node.js is a JavaScript runtime environment available on backend. It is event driven, non-blocking I/O, fast and lightweight. `npm` (Node Package Manager) is well known for its vast ecosystem of libraries and module, it install the package globally. While `npx` runs package without installing them globally.

Node.js uses `.js` file extension. But to use Es modules, `.mjs` is used as file extension. `.js` use `require()` to require, `module.exports` to export. `.mjs` use `import` and `export`. Set `"type": "module"` in `package.json` to use module if you're using `.js`

Run `npm init -y` to generate `package.json` that record npm dependencies and metadata

Example of a basic web server using node.js

```js {title="server.js"}
// Import the built-in modules
const http = require('http');
const fs = require('fs');
const path = require('path');
const PORT = 3000;
const FILE_PATH = './picture.jpg';

// Create an HTTP server
const server = http.createServer((req, res) => {
  const filePath = path.join(__dirname, FILE_PATH);
  fs.readFile(filePath, (err, data) => {
    if (err) {
      res.writeHead(404);
      res.end('File not found!');
      return;
    }
    // Browser will allow request made to different domain
    res.setHeader("Access-Control-Allow-Origin", "*");
    res.setHeader("Access-Control-Allow-Methods", "POST, GET, PUT");
    res.setHeader("Access-Control-Allow-Headers", "Content-Type");
    res.writeHead(200, { 'Content-Type': 'image/jpg' });
    res.end(data);
  });
});

// Define a port and start the server
server.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}`);
});
```

Run the server using this command

```bash
node server.js
```

To run multiple server at same time

```js {title="package.json"}
{
  "scripts": {
    "start:hugo": "hugo server",    // Replace hugo with your actual package
    "start:node": "node server.js", // Replace "server.js" with your actual Node server file name
    "start": "concurrently \"npm run start:hugo\" \"npm run start:node\""
  }
}
```

#### Express.js

<div style="margin: 3rem">
{{< inline-svg src="svgs/logos/express.svg" width="192px" height="79px" class="svg-inline-custom" >}}
</div>

Express.js is a minimal web framework for Node.js, designed to simplify building web applications and APIs.

{{< link-card
  title="Express.js"
  description="Explore how Express.js works!"
  href="/docs/web/express.js/"
>}}

#### Django

<div style="margin: 3rem">
{{< inline-svg src="svgs/logos/django.svg" width="192px" height="79px" class="svg-inline-custom" >}}
</div>

Django is a high-level Python web framework that enables rapid development of secure and maintainable web applications. Comes with built-in admin panel, and user authentication. Django have ORM (Object-Relational Mapping) allowing developers work with database without writing raw SQL and uses MVT architecture.

- Model: Represents the data structure and database schema. It defines the shape of the data and handles database queries via Django's ORM.
- View: Handles the logic for what data is presented to the user. Views fetch data from models and send it to templates.
- Template: Responsible for rendering the final HTML that the user sees. Templates receive data from views and format it for display.

#### PHP

<div style="margin: 3rem">
{{< inline-svg src="svgs/logos/php.svg" width="192px" height="79px" class="svg-inline-custom" >}}
</div>

PHP (Hypertext Preprocessor) is a popular, open-source server-side scripting language designed primarily for web development. It is widely used to create dynamic and interactive web pages. PHP code is executed on the server, and the result is sent back to the client as plain HTML. PHP works by embedding PHP code within HTML using `<?php ...?>`

### Database

A database used to store datas and can be hosted on different server.

#### SQL

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/mysql.svg" width="192px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/sqlite.svg" width="192px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/postgresql.svg" width="192px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

SQL (Structured Query Language) databases are structured database using tables with rows and columns to store data, and use keys to refer to other table for relation.

| SQL Databases | Feature |
| - | - |
| MySQL | Classic SQL database |
| SQLite | Suitable for smaller database |
| PostgreSQL | Open-sourced supporting relational and object-oriented feature and have string performance |

#### NoSQL

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/mongodb-icon.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/firestore.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/redis.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/neo4j.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

NoSQL Databases are suitable for unstructured data. Often used for real-time and distributed system.

| NoSQL Databases | Feature |
|-|-|
| MongoDB | For document store |
| Firestore | Google cloud |
| Redis | Key-value store |
| Neo4j | Graph database |

### Tech Stack

A tech stack refers to a set of tools, programming languages, and technologies that work together to build digital products or solutions such as websites, mobile, and web apps. Frontend tech stack is the client-side appplication such as visual appereance. Backend is the server-side software developement.

Here are some top models for proven use

#### LAMP

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/linux.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/apache.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/mysql.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/php.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

> Linux, Apache, MySQL, PHP

Cost efficiency, flexibility, performance

#### ASP.NET

> ASP.NET MVC, IIS, Angular, SQL, Azure

For Windows

#### MEAN

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/mongodb-icon.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/express.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/angular.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/nodejs-icon.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

> MongoDB, Express.js, Angular.js, Node.js

JS focused, open source, fast

#### MERN

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/mongodb-icon.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/express.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/react.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/nodejs-icon.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

> MongoDB, Express.js, React, Node.js

MEAN with React as frontend

#### MEVN

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/mongodb-icon.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/express.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/vue.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-3 flex-fill">
          {{< inline-svg src="svgs/logos/nodejs-icon.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

> MongoDB, Express.js, Vue, Node.js

MEAN with Vue as frontend

#### Python

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-6 flex-fill">
          {{< inline-svg src="svgs/logos/python.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-6 flex-fill">
          {{< inline-svg src="svgs/logos/django.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
</div>

> Django

Easy to use

### Legacy Note

<iframe src="/web" width="100%" height="600" style="border:none;"></iframe>

{{< callout note >}} SVG sourced from [Iconduck](https://iconduck.com/sets/stack-icons), [techicons](https://techicons.dev/), [svgrepo.com](https://www.svgrepo.com/). [aws-icon](https://aws-icons.com/) {{< /callout >}}