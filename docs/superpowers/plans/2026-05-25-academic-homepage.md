# Academic Homepage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Install al-folio Jekyll theme into existing `Jack414b/Jack414b` repo, configure gray-scale color scheme, migrate README content, and deploy via GitHub Pages.

**Architecture:** al-folio Jekyll theme deployed via GitHub Actions to `gh-pages` branch. Content stored as Markdown/YAML in `_pages/`, `_data/`, and `_bibliography/`. The existing `README.md` stays in place for the GitHub profile page. Site served at `https://jack414b.github.io/Jack414b/`.

**Tech Stack:** Jekyll, al-folio theme, GitHub Actions, GitHub Pages, Docker (local dev)

---

### Task 1: Initialize al-folio theme in repo

**Files:**
- Create: `_config.yml`, `Gemfile`, `Gemfile.lock`, `.github/workflows/deploy.yml`, `docker-compose.yml`, `Dockerfile`
- Create: `_pages/`, `_data/`, `_bibliography/`, `_layouts/`, `_includes/`, `_sass/`, `_posts/`, `_news/`, `_projects/`, `assets/`, `bin/`, `robots.txt`, `404.html`, `index.html`, `CNAME` (placeholder), `purgecss.config.js`, `.gitignore` (update), `.nojekyll`

- [ ] **Step 1: Clone al-folio template and copy files**

```bash
cd /tmp && git clone --depth 1 https://github.com/alshedivat/al-folio.git al-folio-temp
cd /home/devcontainers/jack414b-profile
cp /tmp/al-folio-temp/_config.yml .
cp /tmp/al-folio-temp/Gemfile .
cp /tmp/al-folio-temp/Gemfile.lock .
cp /tmp/al-folio-temp/docker-compose.yml .
cp /tmp/al-folio-temp/Dockerfile .
cp /tmp/al-folio-temp/purgecss.config.js .
cp /tmp/al-folio-temp/robots.txt .
cp /tmp/al-folio-temp/404.html .
cp /tmp/al-folio-temp/CNAME .
cp -r /tmp/al-folio-temp/_pages .
cp -r /tmp/al-folio-temp/_data .
cp -r /tmp/al-folio-temp/_bibliography .
cp -r /tmp/al-folio-temp/_layouts .
cp -r /tmp/al-folio-temp/_includes .
cp -r /tmp/al-folio-temp/_sass .
cp -r /tmp/al-folio-temp/_posts .
cp -r /tmp/al-folio-temp/_news .
cp -r /tmp/al-folio-temp/_projects .
cp -r /tmp/al-folio-temp/assets .
cp -r /tmp/al-folio-temp/bin .
cp -r /tmp/al-folio-temp/.github .
```

- [ ] **Step 2: Update .gitignore**

Add to end of existing `.gitignore` (create if not exists):

```gitignore
_site/
.jekyll-cache/
.jekyll-metadata
vendor/
.bundle/
```

- [ ] **Step 3: Add .nojekyll file**

```bash
touch /home/devcontainers/jack414b-profile/.nojekyll
```

- [ ] **Step 4: Commit al-folio files**

```bash
cd /home/devcontainers/jack414b-profile
git add -A
git commit -m "feat: add al-folio Jekyll theme files"
```

---

### Task 2: Configure `_config.yml` for gray-scale academic site

**Files:**
- Modify: `_config.yml`

- [ ] **Step 1: Configure site settings in `_config.yml`**

Edit `_config.yml` — set these values:

```yaml
title: blank
first_name: Jiale
middle_name:
last_name:
email: JIALE010@e.ntu.edu.sg
description: >
  Undergraduate senior at Nanjing University, incoming graduate student at NTU.
  Research interests: Computer Vision, Multi-modal AI, NeRF & 3DGS, Embodied AI.
url: https://jack414b.github.io
baseurl: /Jack414b
```

- [ ] **Step 2: Configure theme colors to gray-scale in `_config.yml`**

Set color-related settings:

```yaml
enable_darkmode: true

repo_theme_light: default
repo_theme_dark: dark
```

- [ ] **Step 3: Configure navigation in `_config.yml`**

Make sure these collections have `output: true`:

```yaml
collections:
  news:
    defaults:
      layout: post
    output: true
    permalink: /:collection/:title/
  projects:
    output: true
    permalink: /:collection/:title/
```

- [ ] **Step 4: Set optional features in `_config.yml`**

```yaml
enable_masonry: true
enable_math: true
enable_medium_zoom: true
lazy_loading_images: true
search_enabled: true
```

- [ ] **Step 5: Commit configuration**

```bash
git add _config.yml
git commit -m "feat: configure al-folio for gray-scale academic site"
```

---

### Task 3: Customize gray-scale theme styles

**Files:**
- Create: `_sass/_themes.scss`
- Modify: `_sass/_base.scss` (if needed), `assets/css/main.scss`

- [ ] **Step 1: Create gray-scale theme file `_sass/_themes.scss`**

```scss
/*******************************************************************************
 * Gray-scale theme for academic homepage
 ******************************************************************************/

:root {
  // Light mode — warm grays
  --global-bg-color: #ffffff;
  --global-text-color: #2d2d2d;
  --global-theme-color: #555555;
  --global-hover-color: #333333;
  --global-theme-color-rgb: 85, 85, 85;
  --global-footer-bg-color: #f5f5f5;
  --global-footer-text-color: #6c6c6c;
  --global-footer-link-color: #444444;

  --global-divider-color: #e0e0e0;
  --global-card-bg-color: #fafafa;
  --global-code-bg-color: #f4f4f4;

  .block-publications a {
    color: var(--global-theme-color);
  }
}

html[data-theme="dark"] {
  // Dark mode — cool grays
  --global-bg-color: #1a1a1a;
  --global-text-color: #d4d4d4;
  --global-theme-color: #999999;
  --global-hover-color: #bbbbbb;
  --global-theme-color-rgb: 153, 153, 153;
  --global-footer-bg-color: #222222;
  --global-footer-text-color: #999999;
  --global-footer-link-color: #aaaaaa;

  --global-divider-color: #333333;
  --global-card-bg-color: #242424;
  --global-code-bg-color: #2a2a2a;
}
```

- [ ] **Step 2: Verify `_sass/_base.scss` includes theme variables**

Check that `_sass/_base.scss` references `var(--global-theme-color)` for links and accents. If it hardcodes colors, replace them with CSS variables.

- [ ] **Step 3: Commit theme styles**

```bash
git add _sass/_themes.scss
git commit -m "style: add gray-scale theme colors"
```

---

### Task 4: Configure navigation and site data

**Files:**
- Modify: `_data/navigation.yml`, `_data/social.yml`, `_data/contact.yml`

- [ ] **Step 1: Configure navigation `_data/navigation.yml`**

```yaml
header:
  - title: Home
    url: /
  - title: News
    url: /news/
  - title: Publications
    url: /publications/
  - title: Projects
    url: /projects/
  - title: CV
    url: /cv/
```

- [ ] **Step 2: Configure social links `_data/social.yml`**

Remove unused social entries, keep only:

```yaml
- title: Email
  url: mailto:JIALE010@e.ntu.edu.sg
  icon: fas fa-envelope
- title: GitHub
  url: https://github.com/Jack414b
  icon: fab fa-github
- title: Google Scholar
  url: https://scholar.google.com/citations?user=YOUR_ID
  icon: fas fa-graduation-cap
```

- [ ] **Step 3: Commit data files**

```bash
git add _data/navigation.yml _data/social.yml
git commit -m "feat: configure navigation and social links"
```

---

### Task 5: Create content pages from README

**Files:**
- Modify: `_pages/about.md`
- Modify: `_pages/news.md`
- Modify: `_pages/publications.md`
- Modify: `_pages/projects.md`
- Modify: `_pages/cv.md`

- [ ] **Step 1: Write Home/About page `_pages/about.md`**

```markdown
---
layout: about
title: About
permalink: /
subtitle: >
  <div align="center">
  <a href="https://git.io/typing-svg">
    <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=28&duration=4000&pause=1000&color=555555&center=true&vCenter=true&random=false&width=600&lines=Hi%2C+I'm+Jiale+%F0%9F%91%8B;Computer+Vision;Multi-modal+AI;NeRF+%26+3DGS;Embodied+AI" alt="Typing SVG" />
  </a>
  </div>

profile:
  align: right
  image: prof_pic.jpg
  image_circular: true
  more_info: >
    <p>📧 JIALE010@e.ntu.edu.sg</p>
    <p>📍 Nanjing / Singapore</p>

news: true
selected_papers: true
social: true
---

I'm an undergraduate senior at **Nanjing University** (南京大学), School of Electronic Science & Engineering, and an incoming graduate student at **Nanyang Technological University** (NTU), School of EEE.

My research interests span **Computer Vision**, **Multi-modal Learning**, **Large Language Models**, and **Embodied AI**. Currently exploring **NeRF** and **3D Gaussian Splatting** (3DGS) for autonomous driving applications.

---

### 🎓 Education

| | |
|---|---|
| **NTU** — M.Sc. EEE | *Incoming* |
| **NJU** (南京大学) — B.Eng. | *Senior Year* |

---

### 🛠️ Tech Stack

![C](https://img.shields.io/badge/C-00599C?style=flat-square&logo=c&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![ROS](https://img.shields.io/badge/ROS-22314E?style=flat-square&logo=ros&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white)

---

### 📊 GitHub Stats

![Stats](https://github-readme-stats.vercel.app/api?username=Jack414b&show_icons=true&theme=default&hide_border=true&count_private=true)
![Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=Jack414b&layout=compact&hide_border=true&theme=default)
```

- [ ] **Step 2: Write News page `_pages/news.md`**

```markdown
---
layout: page
title: News
permalink: /news/
nav: true
nav_order: 2
---

{% include news.liquid %}

<div class="news">
  <div class="table-responsive">
    <table class="table table-sm table-borderless">
      <tr>
        <th scope="row" style="width: 20%">May 2025</th>
        <td>Accepted to <strong>Nanyang Technological University</strong> (NTU), M.Sc. in EEE</td>
      </tr>
      <tr>
        <th scope="row" style="width: 20%">2025</th>
        <td>Senior year at <strong>Nanjing University</strong> (南京大学), School of Electronic Science & Engineering</td>
      </tr>
    </table>
  </div>
</div>
```

- [ ] **Step 3: Write Publications page `_pages/publications.md`**

```markdown
---
layout: page
title: Publications
permalink: /publications/
nav: true
nav_order: 3
---

{% include bib_search.liquid %}

<div class="publications">
  {% bibliography %}
</div>

<p class="text-muted mt-4">
  <em>Publications will appear here. Currently working on research in NeRF and 3D Gaussian Splatting.</em>
</p>
```

- [ ] **Step 4: Write Projects page `_pages/projects.md`**

```markdown
---
layout: page
title: Projects
permalink: /projects/
nav: true
nav_order: 4
---

<div class="projects">

<div class="row">
  <div class="col-sm-6 mt-3 mt-md-0">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">NeRF & 3DGS Research</h5>
        <p class="card-text">Exploring Neural Radiance Fields and 3D Gaussian Splatting for autonomous driving scene reconstruction.</p>
        <span class="badge bg-secondary">In Progress</span>
      </div>
    </div>
  </div>
  <div class="col-sm-6 mt-3 mt-md-0">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">Multi-modal Learning</h5>
        <p class="card-text">Research on vision-language models and cross-modal understanding.</p>
        <span class="badge bg-secondary">In Progress</span>
      </div>
    </div>
  </div>
</div>

</div>
```

- [ ] **Step 5: Write CV page `_pages/cv.md`**

```markdown
---
layout: cv
title: CV
permalink: /cv/
nav: true
nav_order: 5
---
```

- [ ] **Step 6: Commit content pages**

```bash
git add _pages/about.md _pages/news.md _pages/publications.md _pages/projects.md _pages/cv.md
git commit -m "feat: create content pages with README content"
```

---

### Task 6: Add profile photo placeholder

**Files:**
- Create: `assets/img/prof_pic.jpg`

- [ ] **Step 1: Create placeholder note**

```bash
echo "Place profile photo (prof_pic.jpg) in assets/img/" > /home/devcontainers/jack414b-profile/assets/img/README_photo.txt
```

- [ ] **Step 2: Commit**

```bash
git add assets/img/README_photo.txt
git commit -m "docs: add profile photo placeholder note"
```

---

### Task 7: Configure GitHub Actions for deployment

**Files:**
- Modify: `.github/workflows/deploy.yml`

- [ ] **Step 1: Verify deploy workflow**

Check that `.github/workflows/deploy.yml` pushes to `master` branch triggers:

```yaml
on:
  push:
    branches:
      - master
  pull_request:
    branches:
      - master
```

If it says `main`, change `branches:` to `master`.

- [ ] **Step 2: Commit workflow fix**

```bash
git add .github/workflows/deploy.yml
git commit -m "ci: set deploy workflow to trigger on master branch"
```

---

### Task 8: Push and deploy

- [ ] **Step 1: Push to GitHub**

```bash
git push origin master
```

- [ ] **Step 2: Enable GitHub Pages**

After push, instruct user to:
1. Go to `https://github.com/Jack414b/Jack414b/settings/pages`
2. Set **Source** to "Deploy from a branch"
3. Set **Branch** to `gh-pages` (created automatically by the deploy action)
4. Wait for the deploy action to complete (~4 min)

- [ ] **Step 3: Verify site**

Site should be live at: `https://jack414b.github.io/Jack414b/`

---

### Task 9: Post-deploy verification

- [ ] **Step 1: Check all pages load**

Verify each page returns 200:
- `https://jack414b.github.io/Jack414b/` (Home)
- `https://jack414b.github.io/Jack414b/news/`
- `https://jack414b.github.io/Jack414b/publications/`
- `https://jack414b.github.io/Jack414b/projects/`
- `https://jack414b.github.io/Jack414b/cv/`

- [ ] **Step 2: Verify gray theme**

Check that:
- Light mode shows gray-scale colors (no blue/green/orange accents)
- Dark mode toggle works
- Links and buttons use gray tones

- [ ] **Step 3: Verify README preserved**

Check `https://github.com/Jack414b/Jack414b` still shows the original profile README.
