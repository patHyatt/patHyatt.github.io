# Publishing a New Blog Post

A linear checklist for writing and publishing a new entry on patrickhyatt.com.

---

## 1. Create the post file

Copy the template and name it with today's date:

```bash
cp _posts/_template.md _posts/YYYY-MM-DD-your-post-slug.md
```

**Naming rules:**
- Format: `YYYY-MM-DD-slug.md` (e.g. `2026-02-28-my-new-post.md`)
- Slug: lowercase, words separated by hyphens, no spaces or special characters
- Date: use the date you intend to publish

---

## 2. Fill in the front matter

Open the file and update every field at the top:

```yaml
---
title: "Your Post Title Here"
layout: "post"
date: "2026-02-28 09:00:00 -0500"
description: "One or two sentences shown in search results. Under 155 chars."
keywords: "relevant, comma, separated, keywords"
---
```

- **title** — displayed as the `<h1>` on the post page and in the post list
- **date** — controls sort order; include timezone offset (e.g. `-0500` for EST)
- **description** — used by `jekyll-seo-tag` for `<meta name="description">`
- **keywords** — optional, used for meta keywords

---

## 3. Write the content

Write in standard Markdown. The excerpt separator controls what appears in the post list on the home page:

```markdown
This sentence appears in the post list.

<!--excerpt-->

The rest of the post only appears on the post page itself.
```

Everything before `<!--excerpt-->` is shown on the home page. Put your hook there (1-2 paragraphs max).

---

## 4. Add images (optional)

### Prepare images

1. Create a folder: `assets/img/YYYY/MM/DD/`
2. Export your image at full resolution (JPG or PNG). Aim for under 2 MB before optimization.
3. Run through an optimizer (e.g. [Squoosh](https://squoosh.app) or `imagemagick`) to reduce file size before committing.

### Embed an image

```html
<img
  src="/assets/img/2026/02/28/my-photo.jpg"
  alt="Description of the photo"
  width="800"
  height="600"
  loading="lazy"
  decoding="async"
>
```

Always include `alt`, `width`, and `height` to prevent layout shift and improve accessibility.

---

## 5. Preview locally (optional but recommended)

```bash
bundle exec jekyll serve
```

Visit `http://localhost:4000` to check the post renders correctly, images load, and the excerpt appears properly on the home page.

If this is your first time running locally after the Gemfile update:

```bash
bundle install
bundle exec jekyll serve
```

---

## 6. Commit the post

```bash
git add _posts/YYYY-MM-DD-your-post-slug.md
# If you added images:
git add assets/img/YYYY/MM/DD/
git commit -m "Add post: Your Post Title Here"
```

---

## 7. Push and deploy

```bash
git push origin master
```

GitHub Actions (`.github/workflows/deploy.yml`) automatically builds the Jekyll site and deploys to GitHub Pages. Monitor progress at:

```
https://github.com/patHyatt/patHyatt.github.io/actions
```

The live site updates within 1-2 minutes of the push.

---

## Quick reference

| Task | Command |
|------|---------|
| Create post | `cp _posts/_template.md _posts/YYYY-MM-DD-slug.md` |
| Serve locally | `bundle exec jekyll serve` |
| Commit post | `git add _posts/... && git commit -m "Add post: ..."` |
| Publish | `git push origin master` |
| Check build | GitHub → Actions tab |

