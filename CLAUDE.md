# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ADA Corporate Hub is a static HTML/CSS/JavaScript single-page application for Abu Dhabi Aviation's internal corporate intranet portal. It features multiple UI design variants for the same corporate hub interface.

**Tech Stack:** Vanilla HTML, CSS3, JavaScript (no build tools or frameworks)
**Hosting:** Vercel

## Development

This is a pure static site with no build process:

- **Run locally:** Open `index.html` in a browser or use a local HTTP server
- **Deploy:** Push files to Vercel (deployment is automatic)

No linting, testing, or build commands are configured.

## Architecture

### View System

`index.html` acts as a router/shell that dynamically loads different corporate hub views:

- **Option 1 (Corporate View):** `ada-corporate-hub.html` - Traditional light theme with ADA red branding
- **Option 2 (Command Center):** `option 2.html` - Bento-box card layout with live clock
- **Option 3 (Aurora View):** `option 3.html` - Dark theme with purple/green aurora palette
- **Option 4 (Sky View):** `option 4.html` - Blue glassmorphism theme with animated backgrounds

The view switcher in `index.html`:
1. Fetches the selected HTML file via `fetch()`
2. Extracts `<style>`, `<script>`, and body content using regex
3. Injects styles into `<head>` with `data-view` attributes
4. Injects body HTML into a container div
5. Executes scripts in the loaded view's context
6. Persists view preference in localStorage

### Department Pages

- `ada-flight-ops.html` / `flight-ops.html` - Flight Operations portal
- `ada-it-department.html` / `it-department.html` - IT Department portal

Navigation links in loaded views are dynamically updated to route to these department pages.

### Page Structure

All pages follow this structure:
1. **Header:** Logo, search, notifications, user profile
2. **Navigation:** Sticky menu with dropdown support
3. **Main Content:** News, announcements, alerts, department grid
4. **Sidebar:** Quick links, resources
5. **Footer:** Company info and links

## Design System

**Brand Colors:**
- `--ada-red: #C8102E` (primary)
- `--ada-charcoal: #58585A`
- `--ada-dark-gray: #333333`

**Spacing (8px base):** xs=4px, sm=8px, md=16px, lg=24px, xl=32px, xxl=48px

**Typography:**
- Traditional views: Roboto
- Aurora View: Outfit/Inter
- Sky View: Sora/DM Sans

All styles are embedded in `<style>` tags within each HTML file (no external stylesheets).

## Vercel Configuration

`vercel.json` enables clean URLs and SPA routing - all root requests route to `index.html`.
