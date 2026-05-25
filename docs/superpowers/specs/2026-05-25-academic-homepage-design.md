# Academic Homepage Design

## Overview

Convert `Jack414b/Jack414b` into a GitHub Pages academic homepage using the **al-folio** Jekyll theme with a gray-scale color scheme.

## Architecture

- **Theme**: al-folio (Jekyll-based, deployed via GitHub Pages)
- **Deployment**: GitHub Pages from `master` branch root
- **Content format**: Markdown + YAML frontmatter (al-folio convention)
- **README.md**: preserved as-is for GitHub profile page

## Pages & Content

| Page | Content Source |
|------|---------------|
| Home | README: About Me, Education, Tech Stack, Contact, Typing SVG, GitHub Stats, Giphy |
| News | Academic updates (admissions, papers, milestones) |
| Publications | Paper list (placeholder initially, BibTeX-ready) |
| Projects | Project cards (NeRF/3DGS etc., placeholder initially) |
| CV | Online resume page |

## Visual Design

- **Color scheme**: gray-scale (grays, charcoal, white, black accents)
- **Theme toggle**: al-folio built-in light/dark mode
- **Typography**: al-folio defaults (sans-serif, academic style)
- No blue or other accent colors — clean monochrome

## Files to Create/Modify

1. **al-folio files** — `_config.yml`, `_pages/`, `_data/`, `_layouts/`, `_sass/`
2. **Content pages** — about, news, publications, projects, cv
3. **Assets** — profile photo placeholder
4. **README.md** — unchanged

## Deployment

- Push to `master` → GitHub Pages auto-deploys
- Site URL: `https://jack414b.github.io/Jack414b/` (or custom domain later)

## Scope Boundaries

- **In scope**: al-folio setup, gray theme customization, content migration from README, GitHub Pages deployment
- **Out of scope**: custom domain, blog posts, actual publication entries, CI/CD beyond GitHub Pages default
