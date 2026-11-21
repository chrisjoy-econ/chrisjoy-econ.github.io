# CLAUDE.md

Personal academic site for **Christopher J. Joy**, an economic researcher and consultant at Allegheny Economic Research (Pittsburgh). Live at https://chrisjoy-econ.github.io.

## Stack

- **Astro v5**, static output (`astro.config.mjs`). No UI framework, no adapter, no Tailwind or Bootstrap.
- **Custom CSS only**, all in `src/styles/global.css`.
- Deployed to **GitHub Pages** by `.github/workflows/deploy.yml` on every push to `main` (Node 20, `npm ci` → `npm run build` → `dist/`).

## Commands

```sh
npm run dev       # local dev server (http://localhost:4321)
npm run build     # production build to dist/; run this before committing
npm run preview   # serve the built dist/
```

## Structure

```
src/
  layouts/BaseLayout.astro   # <head>, nav, footer; every page wraps in this
  pages/index.astro          # /         About: bio, Working Life, Education, Currently
  pages/research.astro       # /research Research & Writing list (tagged items)
  pages/cv.astro             # /cv       Inline CV + PDF download button
  styles/global.css          # the whole design system
public/                      # favicons, apple-touch-icon, cv.pdf (served at root)
```

Root-level `favicon-*.png` and `assets/` are leftovers from the old Bootstrap site; Astro serves from `public/`. Leave them alone unless asked to clean up.

`align.md` (untracked) is a one-off prompt file for a past copy edit, not part of the site.

## Design rules

- **Minimal academic look.** A single centered column (`--measure: 680px`), EB Garamond body at 18px / 1.75 line height, system sans-serif for nav and labels.
- **Use the CSS variables**, not hard-coded colors: `--bg #fafaf8`, `--fg #1a1a1a`, `--accent #c0303a`, `--muted #6b6b6b`, `--font-body`, `--font-ui`.
- Put new styles in `global.css` and reuse the existing classes (`page-header`, `subtitle`, `rule-accent`, `research-list` / `research-tag` / `research-title` / `research-desc`, `cv-section` / `cv-entry` / `cv-bullets`, etc.) before adding new ones.
- **Lowercase** for the site name, nav links, page `<title>`s and the tagline (`christopher j. joy`, `about · research · cv`). Section `<h2>`s on the About page use Title Case ("Working Life", "Currently").
- Page titles follow the pattern `"<page> — christopher joy"`.
- Escape HTML entities in Astro markup (`&amp;`, `&middot;`, `&mdash;` or a literal —).
- Keep it dependency-free. Don't add packages, JS frameworks or client-side scripts unless asked.
- Prettier: 2-space indent, no tabs (`.prettierrc`).

## Content rules

- **Positioning:** lead with *quantitative / labor-market economist and data analyst*. Southeast Asia is a supporting research interest, not the headline. The tagline is `researcher · consultant · economics & data`.
- **Contact email:** `chrisjoy@fastmail.com`. (The old `chrisjoy@sent.com` should no longer appear anywhere.)
- **Tools named in copy:** Stata, R, Python, SQL.
- **Don't invent content:** publications, dates, degrees, employers or claims. Christopher supplies the copy, and placeholders should be flagged, not filled in.
- Keep his voice: first person, plain and understated, no marketing language.
- Vietnamese place names keep their diacritics (Hà Nội, Việt Nam / Viet Nam).
- The **CV download** button in `cv.astro` points to a OneDrive share link, not `public/cv.pdf`. When the CV changes, the user updates that link; ask which one to use if unclear.
- The footer year is hard-coded in `BaseLayout.astro`. Update it when the year changes.
- Don't edit `research.astro` content unless explicitly asked.

## Git workflow

- `main` is the deploy branch, so **never commit straight to `main`**. Work on a feature branch and open a PR.
- Run `npm run build` and check that it succeeds before committing.
- Never commit `dist/`, `.astro/` or `node_modules/` (already in `.gitignore`).
- Commit messages: short imperative summary (e.g. "Update CV PDF download link").
