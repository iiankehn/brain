# Websites

All plain HTML/CSS on GitHub Pages from `main`. No framework, package manager or
build step. Dark-only modern Metro design; `landing` holds the canonical shared
design and each site has its own accent. Always preserve `CNAME`.

| Site | Repo | Domain | Accent | Purpose |
|---|---|---|---|---|
| CORE | `coredotcom` | core.iiankehn.com | teal `#64d8c8` | Tech news publication ("field notes") |
| CORE Dev | `core-dev` | dev.iiankehn.com | — | Release and development journal |
| Landing | `landing` | www.iiankehn.com | warm amber | Personal site, project list |
| Acute Web | `acute-web-android/docs` | acute.iiankehn.com | CORE blue | Product downloads |

## CORE website (`coredotcom`)

`BUILD_NOTES.md` in the repo is the authoritative style and publishing guide;
the `core-story` skill in that repo follows it. Key facts:

- Posts in `posts/*.html`, copied from `templates/post-template.html`.
- Sequential "Field note NNN" numbering, dated by the source's publication date.
- Featured art: WebP 1672 × 941 in `assets/images/`, shared by card and article.
- Homepage cards are written by hand in `index.html`, newest first.
- Stylesheet cache-busting query string must be bumped on every page after CSS changes.
- Approved recurring sources: The Verge, Thurrott, AppleInsider, 9to5Mac,
  9to5Google, Windows Central, Apple Newsroom.
