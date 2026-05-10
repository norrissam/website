# Sam Norris's personal academic website

Static site, plain HTML/CSS, no build step. Hosted on GitHub Pages from this repo (`norrissam/website`) with custom domain `www.samuel-norris.com`.

## Files

- `index.html` — landing page: intro, working papers, publications.
- `teaching.html` — course list. Currently ECON 594 (Masters thesis, Summer 2026).
- `style.css` — single stylesheet for both pages.
- `sam.jpg` — header portrait, 800px wide, ~120KB. Original is at `/Users/norris/Dropbox/Website/Pictures/SamNorris.jpg` (4MB) — resize with `sips -Z 800 -s formatOptions 85 <src> --out sam.jpg` if replacing.
- `syllabus.pdf`, `lectures/L*.pdf` — course materials, served directly from the repo.
- `CNAME` — contains `www.samuel-norris.com`. Required by GitHub Pages for custom domain.

## Paper entry format

All entries (working papers + publications) follow one shape:

```
<Title-as-link> (with coauthors), <Journal> (<year>)
```

Variants:
- No coauthors: `<Title>, <R&R info>` (e.g. Examiner Inconsistency)
- No journal/R&R: `<Title> (with X)` (e.g. Conviction)
- R&R: `<Title> (with X), revise and resubmit at <Journal>` (lowercase, italicized journal)
- Year is in parens; journal is italicized.
- **No trailing period** on the main entry line.

Extras (non-technical summaries, media coverage) go inside `<span class="extras">` after the main line — those are muted/smaller and *do* end with periods.

## Adding a new paper

1. Add `<li>...</li>` in the right section of `index.html` (working papers are reverse-chronological by status; publications are reverse-chronological by year).
2. Use the format above.
3. PDF link: prefer Sam's Dropbox links (he hosts everything there). Format: `https://www.dropbox.com/.../paper.pdf?raw=1` — the `?raw=1` makes it download directly.

## Adding a lecture

1. Drop the PDF in `lectures/` (clean filename: `L5.pdf`, not `L5 -- Topic.pdf`).
2. In `teaching.html`, change the corresponding `<li>` line to wrap the title in `<a href="lectures/L5.pdf">…</a>`.

## CSS conventions

- Font: Source Serif 4 (Google Fonts) with Charter/Georgia fallbacks. Single family; weight does the hierarchy.
- Max content width: 720px (`--max`).
- Color tokens in `:root`: `--text`, `--muted`, `--accent`, `--rule`, `--bg`.
- Two list classes:
  - `.papers` — used on index.html. First link in each `<li>` is medium weight (works because the title pairs with normal-weight metadata).
  - `.lectures` — used on teaching.html. Whole `<li>` is one link, so weight is normal (otherwise the whole row reads as bold).
- `h2` is the main section header (border-bottom rule). `h3` is a lighter subsection header (no rule, dark text).

## Deployment

Push to `main`; GitHub Pages auto-deploys within ~1 minute. Settings: https://github.com/norrissam/website/settings/pages

The github.io URL (`https://norrissam.github.io/website/`) **redirects to the custom domain** because of the `CNAME` file — there's no easy way to preview the deployed site separately from the live domain. For previews, just open the local files in a browser; they're identical to what gets served.

## DNS

Domain registrar: **Squarespace** (migrated from Google Domains in 2023; nameservers still show `googledomains.com`). Manage at https://account.squarespace.com/domains.

Records that route to GitHub Pages:
- `www` CNAME → `norrissam.github.io`
- `@` four A records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` (these make apex redirect to www).

Don't touch MX records (email) or TXT records (Google verification, SPF, etc.). The `gv-*.dv.googlehosted.com` CNAME is a Google domain-verification record — leave it alone.
