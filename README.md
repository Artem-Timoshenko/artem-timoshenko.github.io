# artemtimoshenko.com — Jekyll source

A single-page academic site built on the **Hardcover** design and hosted on **GitHub Pages**.

## Repository layout

```
new_website/
├── _config.yml                 # Site metadata + plugins
├── Gemfile                     # Pinned to the github-pages gem
├── CNAME                       # Custom domain (artemtimoshenko.com)
├── 404.html                    # Custom 404 in the same style
├── favicon.ico
├── index.html                  # Single page; pulls in all sections
│
├── _data/
│   ├── profile.yml             # Name, email, social, photo, CV path
│   ├── papers.yml              # Newest first; status: wp | fc | pub
│   ├── honors.yml              # Newest first
│   ├── teaching.yml            # Course list
│   └── consulting.yml          # Practice areas + engagement formats
│
├── _layouts/
│   └── default.html            # Sticky masthead, fonts, footer, content slot
│
├── _includes/
│   ├── hero.html               # About / portrait
│   ├── research.html           # Papers list + show-more button
│   ├── consulting.html         # Two-column grid + email CTA
│   ├── teaching-honors.html    # Side-by-side teaching/honors
│   └── section-title.html      # Shared kicker + h2
│
└── assets/
    ├── css/main.css            # All styles in one file (CSS custom props)
    ├── img/Artem T Photo.jpeg
    ├── cv/Timoshenko CV May 2026.pdf
    └── papers/                 # Working-paper PDFs
```

## Editing content

You almost never need to touch HTML — most updates are YAML edits in `_data/`.

- **Add a paper** → prepend an entry to `_data/papers.yml`. Fields:
  - `year` (number), `status` (`wp`, `fc`, or `pub`), `title`, `authors` (list), `venue`, `tldr` (optional, can leave `""`), `links: { pdf | doi | ssrn | bib }` (any subset).
  - The author whose name matches `profile.name` (Artem Timoshenko) is automatically rendered in italic.
- **Add an honor** → prepend to `_data/honors.yml`.
- **Update the CV** → drop the new PDF into `assets/cv/`, then point `cv:` in `_data/profile.yml` at it.
- **Edit copy** (bio, eyebrow tagline, location) → `_data/profile.yml`.
- **Adjust consulting copy** → `_data/consulting.yml` (lede uses raw HTML — `<em>` works).

## Local testing with Jekyll

These steps assume macOS with a working Ruby (3.x). The `Gemfile` pins the `github-pages` gem so your local environment matches what GitHub Pages actually builds with.

```bash
# One-time setup, from the new_website/ folder
cd new_website
bundle install

# Serve locally with live reload
bundle exec jekyll serve --livereload
# → http://127.0.0.1:4000
```

Common flags worth knowing:

```bash
bundle exec jekyll serve --livereload --open-url   # opens browser
bundle exec jekyll serve --drafts                  # if you ever add _drafts/
bundle exec jekyll build                           # one-shot build → _site/
```

If you run into Ruby version issues, install **rbenv** or **chruby** and use Ruby 3.2+. The `webrick` gem in the `Gemfile` keeps `jekyll serve` working on Ruby 3.x (Ruby ≥3 dropped webrick from the stdlib).

To stay in sync with GitHub Pages' Jekyll version over time:

```bash
bundle update github-pages
```

## Deploying to GitHub Pages

GitHub Pages can build this directly — no GitHub Actions config needed.

1. Commit and push the contents of `new_website/` to the **root** of your `artemtimoshenko.github.io` (or whichever) repo. (If you keep `new_website/` as a subfolder of the repo, GitHub Pages won't find it — the Jekyll source has to be at the repo root, or you'll need a custom Actions workflow.)
2. In the repo on GitHub: **Settings → Pages → Source = "Deploy from a branch"**, branch `main` (or `gh-pages`), folder `/` (root).
3. Confirm the **Custom domain** is set to `artemtimoshenko.com` (the `CNAME` file in this repo also sets it).
4. Wait ~1 minute for the build, then check the Actions tab for build status.

## Design tokens (cheat-sheet)

If you ever need to tweak the look, every color and layout dimension is a CSS custom property at the top of `assets/css/main.css`:

```css
--paper:      #f7f3ec;   /* page background */
--paper-deep: #efe9de;   /* button hover, portrait fallback */
--ink:        #1c1814;   /* primary text */
--ink-soft:   #5a5247;   /* secondary text */
--accent:     #7a2e1f;   /* oxblood — eyebrows, hover, "forthcoming" */
--rule:       rgba(28, 24, 20, 0.16);
--rule-soft:  rgba(28, 24, 20, 0.08);
--page-pad-x: 96px;      /* horizontal padding (auto-shrinks on mobile) */
```

Single typeface: **Source Serif 4** from Google Fonts. Italic is load-bearing — used for eyebrows, role line, year/level labels, the email CTA, and the footer.
