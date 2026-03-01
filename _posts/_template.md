---
title: "Your Post Title Here"
layout: "post"
date: "YYYY-MM-DD HH:MM:00 -0500"
description: "One or two sentence description shown in search results and social previews. Keep it under 155 characters."
keywords: "comma, separated, keywords, for, this, post"
---

Opening paragraph — this appears in the post list on the home page.
Keep it engaging; it's the hook before the <!--excerpt--> marker below.

<!--excerpt-->

## Section Heading

Body of the post continues here. Standard Markdown works throughout.

### Sub-section

- Bullet list
- Another item

1. Numbered list
2. Another step

**Bold text**, *italic text*, `inline code`.

```python
# Fenced code block with syntax highlighting
def hello():
    print("Hello, world!")
```

> Blockquote for callouts or pull quotes.

---

## Images

### Standard image with lazy loading

```html
<img
  src="/assets/img/YYYY/MM/DD/my-image.jpg"
  alt="Descriptive alt text"
  width="800"
  height="600"
  loading="lazy"
  decoding="async"
>
```

### Linked thumbnail to full image

```html
<a href="/assets/img/YYYY/MM/DD/full.jpg" target="_blank" rel="noopener" aria-label="View full size: description">
  <img src="/assets/img/YYYY/MM/DD/thumbnail.jpg" alt="Description" width="600" height="400" loading="lazy" decoding="async">
</a>
```

---

## Links

[Link text](https://example.com) — standard Markdown link.

External links (open in new tab):
```html
<a href="https://example.com" target="_blank" rel="noopener noreferrer">Link text</a>
```

Link to another post:
```liquid
[Post title]({% post_url YYYY-MM-DD-post-slug %})
```
