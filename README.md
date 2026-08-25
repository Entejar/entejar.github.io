# Entejar Alam — personal site (Quarto)

A fast, minimal Quarto website for research, publications, CV, and a blog on causal
inference & experimentation. Posts are `.qmd` files with **executable** R/Python code,
LaTeX math, and citations — write in Markdown or the visual editor, and code chunks run
and embed their output.

---

## 1. First-time setup

Install [Quarto](https://quarto.org/docs/get-started/) and, for executable posts,
Python (with `jupyter`, `numpy`, `matplotlib`) and/or R. Then edit `_quarto.yml`:

- `site-url`, and your `linkedin` URL in the navbar (GitHub is already `Entejar`).
- Drop your CV at `assets/cv.pdf`.
- Anything in a gold **Edit me** box on a page is a placeholder.

## 2. Write & preview (this is the easy part)

```bash
quarto preview           # live-reloading local site at http://localhost:xxxx
```

Editing feels like a document, not raw markup — open the project in **RStudio** or
**VS Code** and use the **visual editor** (WYSIWYG) if you'd rather not hand-write Markdown.
Nothing you preview is online; it's all local.

### Add a post
1. Make a folder `posts/your-slug/` with an `index.qmd`.
2. Front matter:
   ```yaml
   ---
   title: "Your title"
   description: "One or two sentences — doubles as the blog-index excerpt and your LinkedIn hook."
   date: 2026-09-01
   categories: [causal-inference, experimentation]
   ---
   ```
3. Write. Inline math `$\tau$`, display `$$ ... $$`, and executable chunks:
   ````markdown
   ```{python}
   import numpy as np
   print(np.mean([1, 2, 3]))
   ```
   ````
   Use `{r}` for R. The chunk runs on render and embeds its output/plots.

### The LinkedIn loop
Write the full argument here; post the `description` as your LinkedIn hook plus a takeaway,
then link back — *"full derivation on my site →"*. Blog = deep dive, LinkedIn = front door.

## 3. Preview privately, publish when ready

Your machine only — nothing is online until you publish. Keep the repo **private** while
drafting. When it's final:

```bash
quarto render                 # runs code, updates the _freeze/ cache
quarto publish gh-pages       # one-time: creates the gh-pages branch + _publish.yml
```

After that first publish, the included GitHub Action (`.github/workflows/publish.yml`)
redeploys on every push to `main`. It uses the committed `_freeze/` cache, so it does **not**
re-run your code on CI — always `quarto render` locally and commit `_freeze/` before pushing.
(In the repo, enable **Settings → Actions → Workflow permissions → Read and write**.)

> Note: a GitHub Pages site is public even from a private repo (on Free/Pro). Keep it private
> by not publishing until you're ready — preview locally in the meantime.

## Structure

```
_quarto.yml       site config, navbar, theme (light/dark)
index.qmd         landing page (hero DAG, focus, publications, latest posts)
research.qmd  publications.qmd  cv.qmd  blog.qmd
posts/            one folder per post (index.qmd) + _metadata.yml defaults
listing-row.ejs   custom template for the post lists
theme/            tokens-light.scss · tokens-dark.scss · components.scss
assets/glyph.svg  brand mark (also favicon)
head.html         font links
.github/workflows/publish.yml
```

Dark mode: the light/dark toggle in the navbar is automatic (two themes in `_quarto.yml`).
Math: MathJax (built in). Publications/CV are hand-authored HTML blocks for full control; a
`.bib`-driven publications page is an easy future upgrade.
