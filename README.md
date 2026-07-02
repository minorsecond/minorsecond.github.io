# minorsecond.github.io

Personal portfolio site — spatial epidemiology, public-health GIS, and applied
statistical software. Built with [Quarto](https://quarto.org) and published to
GitHub Pages at <https://minorsecond.github.io>.

## Structure

```
.
├── _quarto.yml                  # site config: nav, theme, formatting
├── index.qmd                    # home
├── about.qmd                    # about
├── projects.qmd                 # project index
├── publications.qmd             # publications & research
├── cv.qmd                       # CV (links to PDF)
├── projects/
│   ├── wnv-thesis.qmd           # WNV thesis case study
│   ├── mesa.qmd                 # MESA case study
│   ├── hazus.qmd                # FEMA Hazus case study
│   └── seuhd-practicum.qmd      # health-department practicum case study
├── assets/
│   ├── css/styles.scss          # theme overrides (SCSS layer)
│   ├── cv/                      # drop ross-wardrup-cv.pdf here
│   └── img/                     # favicon.png and any figures
├── .github/workflows/publish.yml  # GitHub Actions: render + deploy
├── .gitignore
└── README.md
```

Rendered output goes to `_site/` (git-ignored).

## Setup

### 1. Create the repository

On GitHub, create a repository named exactly **`minorsecond.github.io`** (owner:
`minorsecond`). The name matters — a `<user>.github.io` repo publishes at
`https://<user>.github.io`. Then push this project to it:

```bash
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin git@github.com:minorsecond/minorsecond.github.io.git
git push -u origin main
```

### 2. Install Quarto

Download from <https://quarto.org/docs/get-started/>, or on macOS:

```bash
brew install --cask quarto
quarto --version
```

No R or Python is required to build this site — the pages are plain Markdown with
no executed code.

### 3. Preview locally

From the project root:

```bash
quarto preview
```

This serves the site at <http://localhost:port> and live-reloads as you edit.
Use `quarto render` to build once into `_site/`.

### 4. Publish to GitHub Pages

Two options — pick one.

**Option A — GitHub Actions (recommended, hands-off).**
The included workflow at `.github/workflows/publish.yml` renders and deploys on
every push to `main`. To enable it once:

1. Push this repo to GitHub (step 1).
2. In the repo: **Settings → Pages → Build and deployment → Source** →
   select **GitHub Actions**.
3. Push to `main`. The Actions tab shows the build; the site goes live at
   <https://minorsecond.github.io>.

**Option B — `quarto publish` (manual, from your machine).**
Renders locally and pushes the output to a `gh-pages` branch:

```bash
quarto publish gh-pages
```

The first run sets up the `gh-pages` branch and configures Pages for you. Use
this if you'd rather not use Actions. Don't mix the two methods on the same repo.

## Adding content

- **CV PDF.** Put the file at `assets/cv/ross-wardrup-cv.pdf`; the download link
  on the CV page already points there.
- **Favicon / images.** Put `favicon.png` and any figures in `assets/img/`.
  Project pages have commented placeholders for figures.
- **Publications.** Fill in the sections in `publications.qmd` — the entry
  templates are in HTML comments.
- **New project page.** Add `projects/<name>.qmd` and link it from
  `projects.qmd`.

## Custom domain (optional, later)

You can point a custom domain at the site whenever you're ready — no domain is
required now.

1. Add a file named **`CNAME`** at the repo root containing only your domain,
   e.g.:

   ```
   www.example.com
   ```

   (If you use GitHub Actions to deploy, also add the same file so it ends up in
   `_site/` — the simplest way is to keep `CNAME` at the project root; Quarto
   copies root-level `CNAME` into the output. Alternatively set the domain under
   **Settings → Pages → Custom domain**, which creates/manages the `CNAME` for
   you.)

2. At your DNS provider, add the records GitHub documents for apex/`www` domains
   (`A`/`AAAA` records to GitHub's IPs for an apex domain, or a `CNAME` to
   `minorsecond.github.io` for a `www` subdomain).

3. In **Settings → Pages**, enter the domain and enable **Enforce HTTPS** once
   the certificate is issued.

See <https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site>.

## Notes

- The site is fully static — no backend or server-side code.
- `site-url` in `_quarto.yml` is set to `https://minorsecond.github.io`; update
  it if you move to a custom domain.
