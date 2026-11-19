# Local Minima

The personal blog of **Jalil Farid** — essays on software engineering, statistics,
and the economics of technology.

## Stack

- [Jekyll](https://jekyllrb.com/) 4 with kramdown + Rouge
- Hand-written CSS in `css/style.css` (no framework, no build step)
- Oswald / Inter / JetBrains Mono via Google Fonts
- One tiny inline script for the mobile navigation

## Local development

Install Jekyll once, then serve the site:

```bash
gem install jekyll webrick
jekyll serve --livereload
```

Then open <http://127.0.0.1:4000>.

Production build:

```bash
jekyll build   # writes to _site/
```

## Writing a post

Add a file to `_posts/` named `YYYY-MM-DD-title.md`:

```yaml
---
layout: post
title: The title that appears in the list
snip: One line of context under the title
---

Body copy in Markdown.
```

The post URL follows Jekyll's default `/:categories/:year/:month/:day/:title.html`,
so existing links keep working.

## Structure

```
_layouts/     default, page, and post shells
_includes/    head, navigation, footer, analytics
_posts/       the essays
about/        about page
assets/       contour artwork and favicon
css/style.css the entire theme
```

## License

BSD-2-Clause — see [LICENSE](LICENSE).
