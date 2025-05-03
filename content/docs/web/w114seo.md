---
title: "SEO"
description: ""
summary: ""

date: 2025-03-08T15:48:39+08:00
lastmod: 2025-03-08T15:48:39+08:00
draft: false
weight: 114
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### SEO

Add more information on the site for search engines to crawl to have a better rank.

#### Sematic HTML

Use named tag instead of `div`, `span` tags for better accessibility.

| Tag |Purpose |
| ---- | ---- |
| `<header>` | Introductory content or navigation links at the top of a section or page |
| `<nav>` | Contains navigation links |
| `<main>` | The main content of the document (unique to the page) |
| `<section>` | A thematic grouping of content, usually with a heading |
| `<article>` | Self-contained content that could stand alone (blog post, news article) |
| `<aside>` | Tangentially related content (sidebars, pull quotes) |
| `<footer>` | Footer for a section or the whole page—often has copyright, links, etc |
| `<figure>` | Groups media with a caption |
| `<figcaption>` | Caption for `<figure>` |
| `<mark>` | Highlights text |
| `<time>` | Represents a specific time or date |

#### Metadata

Metadata tags on head tag of html. Next.js have metadata utilities to boost SEO. Open graph show more information about the page when the link to the page shows a preview card.

```html
<Head>
  <title>Title</title>
  <meta name="description" content="This is what the page is about" />
  <meta property="og:title" content="Post" />
  <meta property="og:description" content="A post about..." />
  <meta property="og:image" content="https://yoursite.com/thumbnail.jpg" />
  <meta property="og:url" content="https://yoursite.com/blog/my-post" />
  <meta property="og:type" content="article" />
</Head>
```

Twitter graph is similar to open graph by changing `og` to `twitter`. Exclusively fot Twitter.

#### URL

A slug is the readable part of a URL and is dynamic, usually based on a title. For example, a title of `Hello World` will have a slug of `hello-world`.

#### Sitemap

A generated `sitemap.xml` tells search engines what pages your site has and how often to crawl them.

#### Tips

- Use clean, descriptive URLs
- Mobile Layouts
- Alt text for images
- Proper heading hierarchy
- Clear, useful, unique, text content
