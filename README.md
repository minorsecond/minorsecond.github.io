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
├── CNAME                        # custom domain: rwardrup.com
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

## Custom domain — rwardrup.com

The site is configured to serve at **`rwardrup.com`**:

- A **`CNAME`** file at the repo root contains `rwardrup.com`, and `_quarto.yml`
  lists it under `project.resources` so Quarto copies it into `_site/` on every
  render (required for the GitHub Actions deploy).
- `site-url` in `_quarto.yml` is set to `https://rwardrup.com`.

Two things still have to happen on GitHub's side to make the domain live:

1. **DNS.** At your domain registrar / DNS provider, point `rwardrup.com` at
   GitHub Pages:
   - Apex (`rwardrup.com`) — four `A` records to `185.199.108.153`,
     `185.199.109.153`, `185.199.110.153`, `185.199.111.153` (and, optionally,
     the matching `AAAA` records for IPv6).
   - `www.rwardrup.com` — a `CNAME` record pointing to
     `minorsecond.github.io`.
2. **GitHub.** After the first deploy, go to **Settings → Pages**, confirm the
   custom domain shows `rwardrup.com`, and enable **Enforce HTTPS** once the
   certificate is issued (can take a few minutes to an hour).

Until DNS propagates, the site is still reachable at
`https://minorsecond.github.io`.

See <https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site>.

## Notes

- The site is fully static — no backend or server-side code.
- `site-url` in `_quarto.yml` is `https://rwardrup.com`. The GitHub repository is
  still named `minorsecond.github.io` (a user-pages repo); the custom domain
  layers on top of it.
