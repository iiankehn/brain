# CORE website

**CORE** (core.iiankehn.com) is a static publication covering phones,
computers, operating systems, software and services. Stories are short,
original "field notes" based on credited reporting.

| | |
|---|---|
| Repository | `iiankehn/coredotcom` |
| Technology | Semantic HTML, one CSS file, a small vanilla JavaScript file; no framework, packages or build step |
| Hosting | GitHub Pages from `main` root; `CNAME` → core.iiankehn.com; DNS on Cloudflare |
| Content | 48 posts in `posts/`, hand-written homepage cards in `index.html` |
| Authoritative guide | `BUILD_NOTES.md` |

## Editorial policy

- Recurring sources: The Verge, Thurrott, AppleInsider, 9to5Mac, 9to5Google,
  Windows Central, Apple Newsroom. Confirm with an official primary source where one exists.
- Original headlines and copy. Credit the original reporting, and separate rumor from confirmed news.
- Check for existing coverage before choosing a story.
- Date posts by the source's publication date.
- Sequential numbering: "Field note NNN" in the overline and "End note NNN" in the footer.
- Typical cadence: batches of two or three stories.

## Design system

A modern interpretation of Microsoft Metro, fixed dark, sharing Landing's
canonical layout with a CORE teal accent.

| Token | Value | Use |
|---|---|---|
| `--bg` | `#101010` | Page background |
| `--surface` | `#1c1c1c` | Cards and raised surfaces |
| `--text` | `#f5f5f5` | Body text |
| `--muted` | `#b0b0b0` | Secondary text |
| `--line` | `#383838` | Dividers |
| `--accent` | `#64d8c8` | Links, focus rings, highlights |
| `--accent-hover` | `#9de8dd` | Link hover |

The font stack starts with Segoe UI Variable and Segoe UI. Breakpoints are 800, 600
and 360 px. Reduced-motion and print styles are included. Focus uses a 2 px accent
outline, and layouts tolerate 200 percent text.

## Page anatomy

- **Every page**: a header with the CORE wordmark and Blog and About links, a
  unique `<main>`, and a compact footer.
- **Homepage card**: `article.project.has-image` with a decorative tile image,
  a date and reading-time tag, an `h3` headline link, a one-sentence summary
  equal to the article deck, and a "Read report" link. Only the first card is not lazy-loaded.
- **Article**: back link, overline, `h1`, deck, byline, a featured figure
  (1672 × 941 WebP), the `.reading` body, a sources aside and an end note.

## Publishing workflow

1. Copy `templates/post-template.html` to `posts/<slug>.html`.
2. Take the next field-note number.
3. Write the post and sources. Add featured art at `assets/images/<slug>.webp` (1672 × 941).
4. Add the homepage card in date order and give the previous first card `loading="lazy"`.
5. Run `python3 tools/check_site.py` (0 errors), then preview locally.
6. Merging to `main` publishes within about a minute.

Claude Code automates this with the `core-story` skill in the repository.

## Known content debt

`python3 tools/check_site.py --all` (2026-10-25) reports 47 legacy issues:
8 featured images not at 1672 × 941, 11 cards missing `loading="lazy"`, and card
summaries that no longer match their article decks.

## Related sites

| Site | Repository | Notes |
|---|---|---|
| Landing, www.iiankehn.com | `landing` | Canonical shared design, amber accent, project listing |
| CORE Dev, dev.iiankehn.com | `core-dev` | Release journal, articles per release |
| Acute Web, acute.iiankehn.com | `acute-web-android/docs` | Download site, updated by the release workflow |
