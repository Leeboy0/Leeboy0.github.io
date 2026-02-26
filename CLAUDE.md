# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static cyberpunk-themed personal portfolio site for Boyi Li-Vera (ECE grad student, UC Irvine). No build system, no package manager — pure HTML/CSS/JS deployed directly to GitHub Pages.

To preview locally, open any HTML file directly in a browser or use a simple static server:
```
python -m http.server 8080
```

## Architecture

Three main pages, each with a dedicated CSS file:

| Page | HTML | CSS |
|------|------|-----|
| Landing | `index.html` | `home.css` |
| About | `about.html` | `about.css` |
| Projects | `projects.html` | `projects.css` |

`cyberpunkart.html` exists but is not linked from navigation and has not been updated with owner's content.

**External scripts** (CDN, loaded on about/projects only):
- jQuery 3.1.0 — scroll counter
- GSAP TweenMax 1.11.4 — animation library (loaded but scroll counter uses jQuery)

`main.js` is currently empty (1 line).

## Layout System

All pages use **absolute pixel positioning** for desktop, with `@media` breakpoints overriding positions at:
- `max-width: 480px` (small mobile)
- `360px–765px` (mobile/tablet)
- `768px–1024px` (tablet)
- `1030px–1366px` (small desktop/laptop)
- `1370px–1630px` (medium desktop)
- No breakpoint for `>1630px` (default absolute positions apply)

**Critical pattern**: When adjusting an element's position at a breakpoint, you typically need to update `top`, `left`, and sometimes `transform: scale()` independently per breakpoint. The footer often needs `!important` overrides at the end of each CSS file to fight the original absolute-positioned values.

## Design System

- **Font**: Blender Pro — `font-weight: 200` = Bold, `font-weight: 100` = Book
- **Colors**: yellow `#FCEE09`, red `#FD3649`, cyan `#00E6F6` / `#00F0FF`, dark bg `#020106`
- **Active nav link**: highlighted yellow on each page via `.nav-wrapper ul li:nth-child(N) a` (child 1 = Home, 2 = About, 3 = Projects)
- **Glitch effect on h1**: `home.css` `.glitch` class with `data-text` attribute — hover triggers `glitch-anim-1` / `glitch-anim-2` keyframes
- **Glitch button**: `button::after` with `clip-path` CSS variables and `@keyframes glitch`
- **Scroll progress bar**: fixed right-side 1px vertical bar (`.percent` / `.fill`) driven by inline jQuery script on about/projects pages
- **Background**: animated `Home Page/loop.gif` on index only; `#020106` solid on other pages

## Content Structure

**about.html** skills layout:
- `.languages h2` → "RTL & Scripting" label (yellow, `top: 430px`)
- `.skill_list` → white text pills (`top: 480px`)
- `.software h2` → "Hardware Design & EDA" label (yellow, `top: 610px`)
- `.skill_list2` → cyan `#00F0FF` text pills (`top: 660px`)

**projects.html** card layout:
- `.projects_wrapper` — normal flow container (`margin-top: 360px`, centered, `max-width: 760px`)
- `.section_label` — cyan section divider (`// Experience`, `// Projects`)
- `.card_content` — blurred card (`opacity: 0.45`, `filter: blur(2px)`) → hover reveals (`opacity: 1`, yellow border glow)
- `.card_type` — cyan metadata line
- `.card_title_text` — yellow title
- `.card_body_text p` — white bullet points

## Social Icons

All four social icons (GitHub, YouTube, Instagram, LinkedIn) are present in the DOM on every page. YouTube and Instagram have no `onclick` handler (owner has no accounts for those). GitHub links to `https://github.com/Leeboy0`, LinkedIn to `https://www.linkedin.com/in/boyi-livera/`.

## Resume

`Boyi_LiVera_Resume.pdf` is in the repo root and linked from all pages. If updating the resume, replace this file in place.
