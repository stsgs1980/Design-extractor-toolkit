# Design Extractor Guide

> Extract design systems from live websites using Playwright browser automation.

## Overview

**Design Extractor** анализирует живые сайты и извлекает:

- Tech Stack (framework, CSS, analytics, fonts, icons)
- Design Tokens (colors, typography, CSS variables)
- **Component Detection** (buttons, cards, modals, forms, navigation)
- **Spacing System** (gap, padding, margin patterns, Tailwind detection)
- Screenshots (full page, sections, responsive)
- Layout Information (grid, flexbox)

## Repository

```
GitHub: https://github.com/Sts8987/reverse-engineering-svelte
Local:  C:\Users\stsgr\reverse-engineering-svelte
```

## Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| SvelteKit | 2.x | Framework |
| Playwright | Latest | Browser automation |
| Tailwind CSS | 4 | Styling |
| TypeScript | 5.x | Type safety |
| Bun | 1.x | Package manager |

## Installation

```bash
# Clone repository
gh repo clone Sts8987/reverse-engineering-svelte
cd reverse-engineering-svelte

# Install dependencies
bun install

# Install Playwright browsers
bunx playwright install chromium

# Run development server
bun run dev
```

Open [http://localhost:3001](http://localhost:3001) in your browser.

## Analysis Pipeline

### 7 Stages

```
┌─────────────────────────────────────────────────────────────┐
│ Stage 1: Tech Stack Extraction (20%)                        │
│ ├── Framework: Next.js, Astro, Nuxt, Vite, Webpack         │
│ ├── CSS: Tailwind, Bootstrap, Custom                        │
│ ├── Analytics: GA, PostHog, Hotjar, Clarity                 │
│ ├── Fonts: Primary, Serif, Mono                             │
│ └── Icons: Lucide, Heroicons, Font Awesome                  │
├─────────────────────────────────────────────────────────────┤
│ Stage 2: Section Detection (40%)                            │
│ ├── Navigation (nav, header)                                │
│ ├── Hero (header, .hero)                                    │
│ ├── Content Sections (up to 12)                             │
│ └── Footer                                                  │
├─────────────────────────────────────────────────────────────┤
│ Stage 3: Component Detection (45%) ⭐ NEW                   │
│ ├── Buttons: count, variants, examples                      │
│ ├── Cards: count, patterns                                  │
│ ├── Modals: count, detected                                 │
│ ├── Forms: inputs, selects, textareas                       │
│ ├── Navigation: count, types                                │
│ ├── Icons: count, libraries                                 │
│ ├── Images: count, backgrounds, lazy-loaded                 │
│ ├── Lists: ordered, unordered                               │
│ └── Tables: count, rows                                     │
├─────────────────────────────────────────────────────────────┤
│ Stage 4: Spacing System (50%) ⭐ NEW                        │
│ ├── Gaps: values, most common, patterns                     │
│ ├── Paddings: values, most common                           │
│ ├── Margins: values, most common                            │
│ ├── Spacing Scale: unique sorted values                     │
│ ├── Container Widths: max-width values                      │
│ └── Tailwind Detection: scale matching                      │
├─────────────────────────────────────────────────────────────┤
│ Stage 5: Screenshots (55%)                                  │
│ ├── Full Page (desktop 1280px)                              │
│ ├── Section Screenshots (each detected section)             │
│ └── Responsive:                                             │
│     ├── Tablet (768x1024)                                   │
│     └── Mobile (375x812)                                    │
├─────────────────────────────────────────────────────────────┤
│ Stage 6: Design System (75%)                                │
│ ├── Colors: theme, background, text, used (up to 15)       │
│ ├── Typography: font-family, size, line-height              │
│ ├── CSS Variables: all custom properties                    │
│ └── Animations: animation names used                        │
├─────────────────────────────────────────────────────────────┤
│ Stage 7: Export (90%)                                       │
│ ├── JSON format (data.json)                                 │
│ └── CSS format (optional)                                   │
└─────────────────────────────────────────────────────────────┘
```

## Output Format

### JSON Structure

```json
{
  "meta": {
    "name": "site_name",
    "url": "https://example.com",
    "analyzed_at": "2024-01-15",
    "title": "Page Title",
    "tags": [],
    "page_type": "website",
    "theme": "dark"
  },
  "screenshots": {
    "full": "screenshots/full/desktop_full.png",
    "sections": [
      { "id": "hero", "file": "screenshots/sections/01_hero.png" }
    ],
    "responsive": {
      "tablet": { "viewport": "768x1024", "files": [...] },
      "mobile": { "viewport": "375x812", "files": [...] }
    }
  },
  "tech_stack": {
    "framework": {
      "name": "Next.js",
      "version": "15+",
      "features": ["App Router", "SSR/SSG"]
    },
    "css": {
      "approach": "Tailwind CSS",
      "stats": { "sheets": 5, "rules": 150 }
    },
    "icons": { "library": "Lucide", "icons": [...] },
    "fonts": { "primary": "Inter", "mono": "Roboto Mono" },
    "analytics": [{ "name": "PostHog", "type": "product analytics" }]
  },
  "design_system": {
    "colors": {
      "theme": "dark",
      "background": "rgb(0, 0, 0)",
      "text": "rgb(255, 255, 255)",
      "used": ["rgb(34, 197, 94)", "rgb(59, 130, 246)"]
    },
    "typography": {
      "body_font": "Inter, sans-serif",
      "body_font_size": "16px",
      "body_line_height": "1.5"
    },
    "css_variables": {
      "--primary": "#3b82f6",
      "--background": "#000000"
    },
    "animations": ["fadeIn", "slideUp"],
    "effects": { "backdrop_filter": true }
  },
  "components": {
    "buttons": {
      "count": 12,
      "variants": ["primary", "secondary", "outline"],
      "examples": [
        { "text": "Get Started", "classes": ["btn", "btn-primary"] }
      ]
    },
    "cards": { "count": 8, "patterns": ["card", "feature-card"] },
    "modals": { "count": 2, "detected": true },
    "forms": { "count": 1, "inputs": 5, "selects": 1, "textareas": 0 },
    "navigation": { "count": 2, "types": ["header", "footer"] },
    "icons": { "count": 24, "libraries": ["lucide", "svg"] },
    "images": { "count": 15, "backgrounds": 3, "lazyLoaded": 8 },
    "lists": { "ordered": 0, "unordered": 4 },
    "tables": { "count": 0, "rows": 0 }
  },
  "spacing_system": {
    "gaps": {
      "values": ["16px", "24px", "8px"],
      "mostCommon": "16px",
      "patterns": ["8px grid", "16px base unit"]
    },
    "paddings": {
      "values": ["16px", "24px", "32px"],
      "mostCommon": "16px"
    },
    "margins": {
      "values": ["8px", "16px", "24px"],
      "mostCommon": "8px"
    },
    "spacing_scale": ["4px", "8px", "16px", "24px", "32px", "48px", "64px"],
    "container_widths": ["1280px", "1440px"],
    "is_tailwind": true,
    "tailwind_scale": ["4px", "8px", "16px", "24px", "32px", "48px", "64px"]
  }
}
```

## API Endpoints

### List Sites
```
GET /api/sites
Response: { sites: [...] }
```

### Analyze Site
```
POST /api/analyze
Body: { url: string, name?: string, tags?: string[] }
Response: { success: boolean, siteDir: string }
```

### Get Progress
```
GET /api/analyze?site=NAME
Response: { progress: number, step: string }
```

### Get Screenshots
```
GET /api/screenshots/[siteDir]/[...path]
```

### Delete Site
```
DELETE /api/sites
Body: { siteDir: string }
```

## Usage

### Via Web UI

1. Open http://localhost:3001
2. Click "+ Добавить сайт"
3. Enter URL (e.g., `https://example.com`)
4. Add optional name and tags
5. Click "Анализировать"
6. Watch real-time progress
7. View results in modal

### Via API

```bash
# Start analysis
curl -X POST http://localhost:3001/api/analyze \
  -H "Content-Type: application/json" \
  -d '{"url": "https://example.com", "name": "test"}'

# Check progress
curl "http://localhost:3001/api/analyze?site=test"

# Get results
curl http://localhost:3001/api/sites
```

## GAP Analysis

### ✅ Implemented

| Feature | Status | Description |
|---------|--------|-------------|
| Component Detection | ✅ Done | Buttons, cards, modals, forms, navigation, icons, images, lists, tables |
| Spacing System | ✅ Done | Gap, padding, margin patterns with Tailwind detection |

### 🚧 Still Missing

| Feature | Priority | Description |
|---------|----------|-------------|
| Interaction Patterns | Medium | Hover, focus, transition states |
| Accessibility | Medium | ARIA labels, contrast, focus visible |
| Breakpoints | Low | Actual responsive breakpoints used |

## Output Location

```
reverse-engineering-svelte/
└── download/
    └── design-library/
        └── {site-name}/
            ├── data.json
            └── screenshots/
                ├── full/
                ├── sections/
                └── responsive/
```

## Troubleshooting

### Playwright Issues

```bash
# Reinstall browsers
bunx playwright install chromium

# Check installation
bunx playwright --version
```

### Memory Issues

For large pages, increase Node memory:
```bash
NODE_OPTIONS="--max-old-space-size=4096" bun run dev
```

## Related Documentation

- [Architecture Overview](architecture.md)
- [Library Extractor Guide](library-extractor.md)
- [Template](../templates/design-extractor/template.json)
