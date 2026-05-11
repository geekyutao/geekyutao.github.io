# Maintaining the website

Plain HTML + CSS, hand-edited. No build step, no Jekyll, no Node. Edit `index.html` directly.

## Project layout

```
geekyutao.github.io/
├── index.html              ← homepage (the whole site)
├── style.css               ← all styles
├── images/                 ← photos, publication thumbnails, favicon
├── _legacy/                ← old Jekyll site, kept for reference (delete anytime)
├── .nojekyll               ← tells GitHub Pages NOT to run Jekyll
└── MAINTENANCE.md          ← this file
```

## Previewing locally

```bash
cd geekyutao.github.io
python3 -m http.server 8765
# open http://localhost:8765/
```

You can also just double-click `index.html` to open it in a browser.

## How to update content

Every editable block has a comment above it showing the pattern:

```html
<!-- Publication entry pattern: copy one <article class="pub"> ... </article> block and edit. -->
```

To add a new entry: **find the comment, copy one block below the comment, paste it where you want, edit the text and links.** All styling is automatic.

### Add a publication

1. Open `index.html`, find the `Selected Publications` section.
2. Copy any existing `<article class="pub">…</article>` block.
3. Paste it where it should appear (newest first by convention).
4. Replace title (and its link), author list, venue/year, and the `paper`/`code`/`project` links.
5. To mark yourself as project lead, add the role tag in the venue line:
   ```html
   IEEE RA-L, 2025 · <span class="role-tag">Project Lead</span> · …
   ```
6. To add a short note under the entry (e.g. "Champion of …"), add:
   ```html
   <div class="pub-note">Your note here.</div>
   ```
7. The `[Project Lead]` tag style is in `style.css` under `.role-tag` — change colors there if you want a different look.

### Add an experience / education entry

Find the relevant section, copy a `<div class="exp">…</div>` block, edit the dates, role, organization, and the inline note.

### Add an award

Find the `Selected Awards` section, copy one `<li>` line:
```html
<li><span class="year">2025</span> Your award name</li>
```

### Update your role / tagline

The role appears in three places (search for "Tech Lead"):
- The `<title>` tag at the top
- The `<meta name="description">` and `og:description` tags
- The visible `<p class="role">` line

### Update the hiring blurb

Find the `<p class="callout">` block in the About section. Edit the text — the "Hiring" pill and styling are automatic.

### Update co-author lists

Two publications currently have `<!-- TODO: confirm full co-author list -->` comments — the T-PAMI survey and PvP. Replace `Tao Yu, et al.` with the full list once you've confirmed it.

## Live GitHub stars

The Inpaint Anything star count is fetched from the GitHub API on page load and displayed in the Publications and Projects sections (the `<span id="ia-stars-*">` placeholders).

- Cached in `localStorage` for 6 hours per visitor (no spam).
- Falls back to the hard-coded "7.6k+" if the API call fails (e.g. rate limit, offline).
- To change the cache window, edit the `6 * 3600 * 1000` value in the `<script>` block at the bottom of `index.html`.
- To track stars for a different repo, change the API URL and the placeholder spans.

## Image conventions

- Avatar: `images/hefei.jpg` (cropped to a circle by CSS).
- New images: just drop them in `images/`. Reference them as `images/your-file.png`.
- Recommended formats: JPG for photos, PNG for screenshots/figures.

## Fonts

System fonts only — no Google Fonts call, so the site loads instantly and works offline.

- Body: Charter / Iowan Old Style / Source Serif Pro / Georgia (serif).
- Headings, labels, captions: system sans-serif (San Francisco / Segoe UI / Inter / Helvetica).
- Code / dates: system monospace (SF Mono / Menlo / Consolas).

## Deploying

This is a GitHub Pages user site (`geekyutao.github.io`). Push to the default branch — GitHub will serve `index.html` as-is.

The `.nojekyll` file is important: without it, GitHub tries to interpret `_legacy/` as Jekyll content and will probably fail to build.

## Tidy-up (optional)

- Delete the old Jekyll site: `rm -rf _legacy/` (recoverable from git).
- The README will need updating eventually — it still references the old academic-pages template.

## Adding a blog later

When you're ready for a blog, two low-effort options:

1. **HTML posts** — make a `posts/` folder, each post is its own `index.html`. Link to them from a new "Writing" section in the main page. Zero extra tooling.
2. **Markdown posts** — switch to a small static-site generator like [Eleventy](https://www.11ty.dev/) or [Astro](https://astro.build/). Requires a GitHub Actions workflow but keeps editing in Markdown.

Recommended: stay with HTML until you have ~5 posts; switching later is easy.
