# hannahl8.github.io

Source for [hannahl8.github.io](https://hannahl8.github.io/): my About page, career timeline, and blog. The site is built with [Quarto](https://quarto.org) and served by GitHub Pages from the `docs/` folder.

## Project layout

| Path | What it is |
| --- | --- |
| `index.qmd` | About page: intro, skills, and the academic & career timeline |
| `blog.qmd`, `archive.qmd`, `code-projects-series.qmd` | Listing pages |
| `posts/` | Blog posts, one folder per post (`index.qmd` plus its images) |
| `resume/` | Public resume (`.docx` and `.pdf`) linked from the About page |
| `_quarto.yml` | Site config: navbar, footer, theme, analytics, cookie banner |
| `theme-light.scss`, `theme-dark.scss` | Light/dark themes: fonts, Bootstrap variables, and the `--hl-*` color tokens |
| `styles.css` | Shared styles for both themes (navbar, About page, timeline, listings, posts, cookie banner) |
| `footer-year.html` | Small script that keeps the footer copyright year current |
| `_freeze/` | Saved results of the Python code in the machine learning posts (commit this) |
| `docs/` | Rendered site that GitHub Pages serves (commit this after rendering) |

## Rendering the site

Install [Quarto](https://quarto.org/docs/get-started/), then from the repo root:

```bash
quarto preview   # live preview in the browser while editing
quarto render    # build the full site into docs/
```

Commit the updated `docs/` (and `_freeze/`, if it changed) to publish.

Code in posts is frozen (`freeze: true` in `posts/_metadata.yml`), so a full `quarto render` reuses the saved results in `_freeze/` and doesn't need Python.

## Re-running the machine learning posts

Only needed after you change the code in a post under `posts/machine-learning-intro/`. Set up the Python environment once (Windows PowerShell):

```powershell
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Then render the post you changed. Rendering a single file runs its code and updates `_freeze/`:

```powershell
$env:QUARTO_PYTHON = "$PWD\.venv\Scripts\python.exe"
quarto render posts/machine-learning-intro/regression/index.qmd
```

The charts use the colors defined at the top of each post, which match the site's light theme.

## Common edits

- **Add a timeline entry:** in `index.qmd`, copy a `:::: {.timeline-item ...}` block. Entries alternate `.right` / `.left` starting with `.right` at the top, so flip the classes below a new entry. Add `.current` to the entry you're in now; it gets the "Now" tag.
- **Several roles at one company:** use a `<div class="timeline-roles">` with one `<div class="timeline-role">` per role (see the Estes Express Lines entry). Add `current` to the active role.
- **Skills:** edit the `<li>` badges in the skills block of `index.qmd`.
- **Colors and fonts:** change the variables and `--hl-*` tokens in both theme files so light and dark stay in sync.
