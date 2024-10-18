---
title: "Web Design"
description: ""
summary: ""
date: 2024-10-10T16:43:10+08:00
lastmod: 2024-10-10T16:43:10+08:00
draft: false
weight: 102
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---
### The Web Roadmap

### TECH STACK

#### Bootstrap

A simple CSS framework for easy designing using class by adding the source below

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
```

#### SASS

A CSS preprocessor and will compile to CSS

- .scss have same syntax to css and add more functionality like variable, nesting, mixin(grouping attribute), function
- .sass have similar syntax to python

#### Tailwind CSS

A CSS framework for faster development, similar to bootstrap. But having more configuration space

#### Purge CSS

Remove unused CSS using PostCSS plugin

#### Databse

- MongoDB: storage on document
- SQL: storage on relations

#### Typescript

A language derived from javascript to deal with variable type consistency and typescript compiles to javascript.

### Basic Tutorial

<iframe src="/web" width="100%" height="600" style="border:none;"></iframe>

### Responsive Web Design

RWD is done by flexbox, to control the size of your web elements dynamically

```css
.divContainerClassName {
  display: flex;            /* Enable flexbox */
  flex: 1;                  /* Elements ratio in flexbox */
  flex-wrap: wrap;          /* Elements wrap when there is not enough space */
  flex-direction: row;
  align-items: center;      /* Arrange elements along vertical axis */
  justify-content: center;  /* Arrange elements along horizontal axis */
}
```

{{< details "Example Code" >}}

Source of this web is from a YouTuber [Sajid](https://www.youtube.com/watch?v=FbNvYvTkP64&t=5s&ab_channel=Sajid). View the result [here](/rwd/index.html)

{{< tabs "rwd" >}}

<div style="height:400px; overflow:auto">

{{< tab "html" >}}

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Flexbox Layouts</title>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Montserrat&display=swap"
      rel="stylesheet"
    />
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <div class="flex-cards">
      <div class="c1">
        <div class="card">
          <img class="icons" src="/img/User Experience.svg" />
          <p>
            User <br />
            Experience
          </p>
        </div>
        <div class="card">
          <img class="icons" src="/img/Market research.svg" />
          <p>
            Market <br />
            Research
          </p>
        </div>
        <div class="card">
          <img class="icons" src="/img/wireframes and prototype.svg" />
          <p>
            Wireframes & <br />
            Prototypes
          </p>
        </div>
        <div class="card">
          <img class="icons" src="/img/Visual design.svg" />
          <p>
            Visual <br />
            Design
          </p>
        </div>
        <div class="card2">
          <img class="icons2" src="/img/Research.svg" />
          <p class="p1">Research</p>
        </div>
      </div>
      <div class="c2">
        <div class="card1">
          <img class="logo-icon" src="/img/Logo.svg" />
        </div>
        <div class="card2">
          <img class="icons2" src="/img/Design.svg" />
          <p class="p1">Design</p>
        </div>
      </div>
      <div class="c3">
        <div class="card3">
          <img class="icons1" src="/img/sper fast speed.svg" />
          <p>Super Fast Speed</p>
        </div>
        <div class="card">
          <img class="icons" src="/img/Responsive layouts.svg" />
          <p>
            Responsive <br />
            Layouts
          </p>
        </div>
        <div class="card">
          <img class="icons" src="/img/web security.svg" />
          <p>
            Web <br />
            Security
          </p>
        </div>
        <div class="card2">
          <img class="icons2" src="/img/Development.svg" />
          <p class="p1">Development</p>
        </div>
      </div>
    </div>
  </body>
</html>
```

{{< /tab >}}

{{< tab "css" >}}

```css
:root {
  --ff: "Montserrat", sans-serif;
  --p: 18px/22px var(--ff);
  --p1: 24px/30px var(--ff);
  --colorbody: #fff;
  --colora: #537fe7;
  --colora2: #ffe537;
  --colorp: #1e1e1e;
  --colors: #f2f2f2;
  --shadow: #00000030 0px 0px 10px 0px;
  --transition: 0.3s ease-in-out;
}
body {
  font: var(--p);
  background-color: var(--colorbody);
  color: var(--colors);
  text-align: center;
  margin: auto;
}

p,
.p1 {
  margin: 0;
}
.p1 {
  font: var(--p1);
}

.card,
.card1,
.card2,
.card3 {
  background-color: var(--colorp);
  border-radius: 12px;
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 10px;
  align-items: center;
  justify-content: center;
  transition: var(--transition);
}

.card3:hover,
.card2:hover,
.card1:hover,
.card:hover {
  scale: 1.02;
  box-shadow: var(--shadow);
}

.icons {
  height: 40px;
}
.icons2 {
  height: 32px;
}
.icons1 {
  height: 60px;
}
.logo-icon {
  width: 100px;
}

.flex-cards {
  width: 90%;
  max-width: 1080px;
  margin: 100px auto;
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}

.flex-cards > div {
  flex: 1;
}
.card {
  min-width: 160px;
  height: 165px;
}
.card1 {
  min-width: 330px;
  height: 340px;
}
.card2 {
  min-width: 330px;
  height: 80px;
  flex-direction: row;
}
.card3 {
  min-width: 330px;
  height: 165px;
}

.c1,
.c2,
.c3 {
  display: flex;
  gap: 10px;
  min-width: 330px;
  flex-wrap: wrap;
}
```

{{< /tab >}}

{{< /tabs >}}

{{< /details >}}

### Icons

Discover amazing icon from [fontawesome](https://fontawesome.com/start) and embed into web

#### Figma

Figma is a collaborative web application for interface design. Making layout with autolayout, variable

### Wordpress

A web content management system. Build website on templates easily

javafx, doks, markdown, design, reference, awt, concept
