---
title: "Responsive Web Design"
description: ""
summary: ""
date: 2024-10-19T15:58:18+08:00
lastmod: 2024-10-19T15:58:18+08:00
draft: false
weight: 104
toc: false
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Principle

RWD (Responsive Web Design) is an art of adjusting the size of elements on different screen.

The focus of RWD is designing on mobile layoutting first, then expand to desktop layouyt.

Steps of making basic layoutting

1. Set the body CSS as below

```css
body {
  height: 100vh;
  width: 100vw;
  background-color: black; /* Optional */
  margin: 0rem;
  overflow: hidden; /* Optional */
}
```

2. Make a container. Ensure it inherit the width of the body parent, overflow can be scroll starting at this section.

3. Flexbox inside container

### CSS Flex

Flexbox controls the size of your web elements dynamically

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

### Bootstrap Layoutting

#### Breakpoint

Breakpoint is an important reference to adjust the layout based on device screen width

| Breakpoint|	Class infix |	Dimensions |
| -|- |	- |
| Extra small	| None	 |<576px |
| Small	| sm |	≥576px |
| Medium	| md |	≥768px |
| Large	| lg |	≥992px |
| Extra large	| xl |	≥1200px |
| Extra extra large	| xxl |	≥1400px |

To operate with breakpoints, include the mixins from bootstrap source Sass files

```css
@include media-breakpoint-between(md, xl) { ... }
/* which results in */
@media (min-width: 768px) and (max-width: 1199.98px) { ... }
```

#### Containers

Containers are the most basic layout element in Bootstrap and are required when using the default grid system

- `.container`, which sets a max-width at each responsive breakpoint
- `.container-{breakpoint}`, which is width: 100% until the specified breakpoint
- `.container-fluid`, which is width: 100% at all breakpoints

For example, try to adjust the window width to see the changes below

<div class="custom-box container">container</div>
<div class="custom-box container-md">container-md</div>
<div class="custom-box container-fluid">container-fluid</div>

```html
<div class="custom-box container">container</div>
<div class="custom-box container-md">container-md</div>
<div class="custom-box container-fluid">container-fluid</div>
```

#### Grid

Grid layout divides the screen into 12 equal column. Row must be declared under to provide grid layout, row is a flex.

- `col`, equal column width
- `col-{number}`, number of column taken
- `col-offset-{number}`, offset the col
- `col-{breakpoint}-{number}, use the number of columns after the breakpoint

<div class="container-fluid">
    <div class="row">
        <div class="custom-box col-sm-6 col-lg-8 flex-fill">
            col-sm-6 col-lg-8
        </div>
        <div class="custom-box col-6 col-lg-4 flex-fill">
            col-6 col-lg-4
        </div>
    </div>
    <div class="row">
        <div class="custom-box col-6 col-sm-4 flex-fill">
            col-6 col-sm-4
        </div>
        <div class="custom-box col-6 col-sm-4 flex-fill">
            col-6 col-sm-4
        </div>
        <div class="custom-box col-6 col-sm-4 flex-fill">
            col-6 col-sm-4
        </div>
    </div>
</div>

```html
<div class="container-fluid">
    <div class="row">
        <div class="custom-box col-sm-6 col-lg-8 flex-fill">
            col-sm-6 col-lg-8
        </div>
        <div class="custom-box col-6 col-lg-4 flex-fill">
            col-6 col-lg-4
        </div>
    </div>
    <div class="row">
        <div class="custom-box col-6 col-sm-4 flex-fill">
            col-6 col-sm-4
        </div>
        <div class="custom-box col-6 col-sm-4 flex-fill">
            col-6 col-sm-4
        </div>
        <div class="custom-box col-6 col-sm-4 flex-fill">
            col-6 col-sm-4
        </div>
    </div>
</div>
```

Alignment

<div class="container-fluid">
  <div class="row justify-content-around">
    <div class="custom-box col-3">
      col-3
    </div>
    <div class="custom-box col-3">
      col-3
    </div>
    <div class="custom-box col-3">
      col-3
    </div>
  </div>
</div>

```html
<div class="container-fluid">
  <div class="row justify-content-around">
    <div class="custom-box col-3">col-3</div>
    <div class="custom-box col-3">col-3</div>
    <div class="custom-box col-3">col-3</div>
  </div>
</div>
```

Self alignment

<div class="container">
  <div class="row" style="height: 20vh;">
    <div class="custom-box col align-self-start">One of three columns</div>
    <div class="custom-box col align-self-center">One of three columns</div>
    <div class="custom-box col align-self-end">One of three columns</div>
  </div>
</div>

```html
<div class="container">
  <div class="row" style="height: 20vh;">
    <div class="custom-box col align-self-start">One of three columns</div>
    <div class="custom-box col align-self-center">One of three columns</div>
    <div class="custom-box col align-self-end">One of three columns</div>
  </div>
</div>
```

#### Display

1. Inline: display new elements in one line

```html
<div style="display: inline;">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>

<span>Spans are inline</span>

<div class="d-inline">Child elements are inline</div>
```

2. Block: display new elements in next line

```html
<div style="display: block;">
  <span>1</span>
  <span>2</span>
  <span>3</span>
</div>

<div>divs are inline</div>

<div class="d-inline">Child elements are blocks</div>
```

3. Flexbox

```html
<div style="display: flex;">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>

<span class="d-flex">Display elements in flexbox</span>
```

Adjust flex items horizontally

```html
<div class="d-flex justify-content-start">...</div>
<div class="d-flex justify-content-end">...</div>
<div class="d-flex justify-content-center">...</div>
<div class="d-flex justify-content-between">...</div>
<div class="d-flex justify-content-around">...</div>
<div class="d-flex justify-content-evenly">...</div>
```

Adjust flex items vertically

```html
<div class="d-flex align-items-start">...</div>
<div class="d-flex align-items-end">...</div>
<div class="d-flex align-items-center">...</div>
<div class="d-flex align-items-baseline">...</div>
<div class="d-flex align-items-stretch">...</div>
```

Expand one item only

```html
<div class="d-flex">
    <div class="flex-grow-1">
        <!-- This div grows to take up remaining space in the flex container -->
    </div>
    <div>
        <!-- Fixed-width div that does not expand -->
    </div>
</div>
```

Expand flex items

```html
<div class="d-flex">
    <div class="flex-fill bg-success text-white p-3">Item 1</div>
    <div class="flex-fill bg-primary text-white p-3">Item 2</div>
    <div class="flex-fill bg-warning text-dark p-3">Item 3</div>
</div>
```

#### Bootstrap Utilities

1. Visibility keep the invisible element on the space, but did not show it out

```html
<div class="visible">...</div>
<div class="invisible">...</div>
```

```css
visibility: visible;
visibility: hidden;
```

2. Margin and padding

```html
<div class="p-1">Sets the padding to 1rem</div>
<div class="m-1">Sets the margin to 1rem</div>
```

3. Size

- `w-100` takes 100% of parent's width

#### Conclusion of using Bootstrap

1. Pick a container
2. Put a row and define the column. Commonly use justify, align, w-100
3. Define the child elements of row. Commonly use col-{}, flex-fill, flex-grow