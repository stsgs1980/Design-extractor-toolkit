# Design Extractor Guide

> Extract design systems from live websites using Playwright browser automation.

## Overview

**Design Extractor** анализирует живые сайты и извлекает:

- Tech Stack (framework, CSS, analytics, fonts, icons)
- Design Tokens (colors, typography, CSS variables)
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

### 5 Stages

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
│ Stage 3: Screenshots (55%)                                  │
│ ├── Full Page (desktop 1280px)                              │
│ ├── Section Screenshots (each detected section)             │
│ └── Responsive:                                             │
│     ├── Tablet (768x1024)                                   │
│     └── Mobile (375x812)                                    │
├─────────────────────────────────────────────────────────────┤
│ Stage 4: Design System (75%)                                │
│ ├── Colors: theme, background, text, used (up to 15)       │
│ ├── Typography: font-family, size, line-height              │
│ ├── CSS Variables: all custom properties                    │
│ └── Animations: animation names used                        │
├─────────────────────────────────────────────────────────────┤
│ Stage 5: Export (90%)                                       │
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

### Currently Missing

| Feature | Priority | Description |
|---------|----------|-------------|
| Component Detection | High | Detect buttons, cards, modals, forms |
| Spacing System | High | Extract gap, padding, margin patterns |
| Interaction Patterns | Medium | Hover, focus, transition states |
| Accessibility | Medium | ARIA labels, contrast, focus visible |
| Breakpoints | Low | Actual responsive breakpoints used |

### Planned Improvements

```typescript
// Component Detection (to add)
const components = {
  buttons: document.querySelectorAll('button, .btn').length,
  cards: document.querySelectorAll('.card').length,
  modals: document.querySelectorAll('[role="dialog"]').length,
  forms: document.querySelectorAll('form').length
};

// Spacing System (to add)
const spacing = {
  gaps: new Set(), // '8px', '16px', '24px'...
  paddings: new Set(),
  margins: new Set()
};
```

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
