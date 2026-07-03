# Longevity OS — public demo

## What this is
The de-identified, public **sample** of the Longevity OS dashboard, hosted on GitHub Pages for sharing (Instagram / community). Single self-contained HTML file.

## Stack
- One file: `index.html` — inline HTML + CSS + vanilla JS, no build, no dependencies, no external network calls (fully self-contained; safe under a strict CSP).
- Canvas for gauges/sparklines; theme-aware (light/dark); responsive.

## Structure
```
longevity-os/
├─ index.html   # the entire dashboard (demo/sample data)
├─ README.md
├─ LICENSE
└─ CLAUDE.md
```

## Conventions / rules
- **Demo data only** — never commit real personal health data (name, DOB, real labs/genetics) to this public repo. The private working copy lives outside this repo.
- Keep it a single self-contained file (portability is the point).
- The floating CTA links to the owner's community; placeholder is `https://YOUR-LINK-HERE`.
- Not medical advice — keep the educational disclaimer intact.

## Source of truth
The private full dashboard is maintained at `~/Personal/Health/longevity-os-dashboard.html`; this repo is the sanitized public export.
