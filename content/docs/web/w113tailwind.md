---
title: "Tailwind CSS"
description: ""
summary: ""

date: 2025-03-08T15:48:39+08:00
lastmod: 2025-03-08T15:48:39+08:00
draft: false
weight: 113
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

{{< inline-svg src="svgs/logos/tailwindcss-icon.svg" width="100px" height="79px" class="svg-inline-custom" >}}

Visit official [Tailwind CSS](https://tailwindcss.com/) website for more info.

### Utility Classes

A packed cheatsheet for Tailwind CSS.

```html
<!-- Layouting -->
<div className="flex flex-col items-center justify-center bg-white dark:bg-gray-800"></div>
<div className="grid grid-cols-3 gap-4 hidden text-xl"></div>

<!-- Positioning -->
<div className="relative mx-auto w-full max-w-[400px] space-y-2.5 md:-mt-32"></div>
<div className="leading-loose order-2 group space-x-1"></div>

<!-- Styling -->
<div className="bg-gradient-to-r to-pink-500 from-violet-600 text-white active:rounded-lg focus:shadow-sm hover:border-blue-400"></div>

<!-- Animation -->
<div className="transition-all hover:bg-blue-700 duration-300 ease-in-out"></div>
```

- `md:h-screen`: on medium and up, element height is 100vh
- `max-w-[400px]`: max width is 400px
- `space-y-2.5`: Adds vertical spacing between child elements
- `md:-mt-32`: Apply negative top margin
- `leading-loose`: Control line height to loose
- `order-2`: Put as second order
- `space`: Adds space between siblings, without margin on first/last
- `transition-all`: Smooth transition for all properties
- `group`: A wrapper class to apply hover/focus/whatever styles to child elements

### Breakpoints

| Prefix | Applies at | Devices |
| --- | --- | --- |
| sm | ≥ 640px | Large phone / small tablet (potrait) |
| md | ≥ 768px | Tablet (potrait), phone (landscape) |
| lg | ≥ 1024px | Laptop / tablets (landscape) |
| xl | ≥ 1280px | Desktop |
| 2xl | ≥ 1536px | Large desktop |
