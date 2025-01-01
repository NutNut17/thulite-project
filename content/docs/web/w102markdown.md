---
title: "Markdown"
description: "Markdown are a simple and functional text file that is suitable to be used to make article"
summary: ""
date: 2024-10-08T19:55:19+08:00
lastmod: 2024-10-08T19:55:19+08:00
draft: false
weight: 102
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---
Markdown are a simple and functional text file that is suitable to be used to make article.

This Markdown cheat sheet provides a quick overview of all the Markdown syntax elements edited from [The Markdown Guide](https://www.markdownguide.org)!

### Basic Syntax

#### Heading

Use some # to indicate headings]

```md
# Header 1
## Header 2
```

#### Bold and Italic

```md
**bold text**
--- (This is a horizontal line)
*italicized text*
```

**bold text**

---

*italicized text*

#### Blockquote

```md
>blockquote message
```

> blockquote

#### Ordered List

```md
1. First item
2. Second item
3. Third item
```

1. First item
2. Second item
3. Third item

#### Unordered List

```md
- First item
- Second item
- Third item
  - x
  - y
```

- First item
- Second item
- Third item
  - x
  - y

#### Code

```md
`code` or ``` multiple line codes```
```

`code`

#### Link

```md
[Markdown Guide](https://www.markdownguide.org)
```

[Markdown Guide](https://www.markdownguide.org)

#### Image

```md
![alt text](https://www.markdownguide.org/assets/images/tux.png)
```

![alt text](https://www.markdownguide.org/assets/images/tux.png)

### Extended Syntax

These elements extend the basic syntax by adding additional features. Not all Markdown applications support these elements.

#### Table

```md
| Syntax | Description |
| ----------- | ----------- |
| Header | Title |
| Paragraph | Text |
```

| Syntax    | Description |
| --------- | ----------- |
| Header    | Title       |
| Paragraph | Text        |

#### Footnote

```md
Here's a sentence with a footnote. Look at the footnote at the bottom of the page. [^1]

[^1]: This is the footnote.
```

Here's a sentence with a footnote. Look at the footnote at the bottom of the page. [^1]

#### Heading ID

```md
#### My Great Heading {#custom-id}
```

#### My Great Heading

#### Definition List

```md
term
: definition
```

term
: definition

#### Strikethrough

```md
~~The world is flat.~~
```

~~The world is flat.~~

#### Task List

```md
- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media
```

- [X] Write the press release
- [ ] Update the website
- [ ] Contact the media

#### Emoji

```md
That is so funny! :joy:
```

That is so funny! 😂 (See also [Copying and Pasting Emoji](https://www.markdownguide.org/extended-syntax/#copying-and-pasting-emoji))

#### Highlight

```md
I need to highlight these ==very important words==.
```

I need to highlight these ==very important words==.

#### Subscript and Superscript

```md
H~2~O X^2^
```

H~2~O X^2^

#### Json

```md
```json
    {
      "firstName": "John",
      "lastName": "Smith",
      "age": 25
    }
     ``` (This should be indent to the left)
```

```json
    {
      "firstName": "John",
      "lastName": "Smith",
      "age": 25
    }
```

[^1]: This is the footnote.
