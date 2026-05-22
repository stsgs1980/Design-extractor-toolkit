# Architecture Overview

## System Design

Design Extractor Toolkit следует принципам **Separation of Concerns** и **Anti-Monolith** архитектуры.

## Core Principles

### 1. Separation of Concerns

Каждый инструмент делает **одну** задачу:

```
Design Extractor  → Извлекает design tokens с живых сайтов
Library Extractor → Извлекает компоненты из GitHub репо
UI-Kit Studio     → Создаёт интерфейсы из библиотеки
```

### 2. Anti-Monolith

Инструменты разделены по репозиториям:

| Репо | Назначение |
|------|------------|
| `Design-extractor-toolkit` | Документация и шаблоны |
| `reverse-engineering-svelte` | Design Extractor Engine |
| `zai-ui-kit` | Library Extractor + Component Library |
| `UI-Kit` | Interface Studio (Control Center) |

## Data Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                        DATA FLOW                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  SOURCE 1: Live Website                                        │
│  ┌─────────┐                                                    │
│  │   URL   │─────► Design Extractor ─────► Design Tokens       │
│  └─────────┘           │                   (JSON/CSS)          │
│                        │                                        │
│                        ├── Playwright (browser)                │
│                        ├── Section Detection                   │
│                        ├── Screenshot Generation               │
│                        └── CSS Variables Extraction            │
│                                                                 │
│  SOURCE 2: GitHub Repository                                   │
│  ┌─────────────┐                                                │
│  │  GitHub URL │─────► Library Extractor ───► Components       │
│  └─────────────┘           │                   (npm package)   │
│                            │                                    │
│                            ├── AST Parsing                     │
│                            ├── Component Detection             │
│                            ├── Hook Extraction                 │
│                            └── Token System Extraction        │
│                                                                 │
│  OUTPUT: Unified Design System                                 │
│  ┌─────────────────────────────────────────────────┐           │
│  │  Design Tokens + Components → UI-Kit Studio     │           │
│  └─────────────────────────────────────────────────┘           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## Component Architecture

### Design Extractor (5 Stages)

```
Stage 1: Tech Stack Extraction (20%)
├── Framework Detection (Next.js, Astro, Nuxt, Vite)
├── CSS Approach (Tailwind, Bootstrap, Custom)
├── Analytics (GA, PostHog, Hotjar)
└── Fonts & Icons

Stage 2: Section Detection (40%)
├── Navigation
├── Hero
├── Content Sections (up to 12)
└── Footer

Stage 3: Screenshots (55%)
├── Full Page (desktop)
├── Section Screenshots
└── Responsive (tablet 768px, mobile 375px)

Stage 4: Design System (75%)
├── Colors (theme, background, text, used)
├── Typography (font-family, size, line-height)
├── CSS Variables
└── Animations

Stage 5: Export (90%)
├── JSON format
└── CSS format (optional)
```

### Library Extractor (Planned)

```
Phase 1: Repository Scan
├── Clone repository
├── Parse file structure
└── Identify tech stack

Phase 2: Component Detection
├── React components (.tsx)
├── Vue components (.vue)
├── Svelte components (.svelte)
└── Web components

Phase 3: Extraction
├── Component code
├── Dependencies
├── Hooks
├── Utils
└── Types

Phase 4: Package Generation
├── package.json
├── Index exports
└── TypeScript definitions
```

## Technology Stack

### Design Extractor

| Technology | Purpose |
|------------|---------|
| SvelteKit 2.x | Framework |
| Playwright | Browser automation |
| Tailwind CSS 4 | Styling |
| TypeScript | Type safety |
| Bun | Package manager |

### Library Extractor

| Technology | Purpose |
|------------|---------|
| TypeScript | Implementation |
| AST Parser | Code analysis |
| Z.ai Skill | Integration |

## Integration Points

### UI-Kit Studio Integration

```
UI-Kit Studio (Control Center)
│
├── /extractor (Dashboard Page)
│   ├── Design Extractor UI
│   └── Library Extractor UI
│
├── /library (Component Library)
│   └── Extracted components
│
└── /studio (Interface Builder)
    └── Create from library
```

### API Integration

```
Design Extractor API:
├── POST /api/analyze     → Start analysis
├── GET /api/analyze      → Get progress
├── GET /api/sites        → List analyzed sites
└── GET /api/screenshots  → Get screenshots

Library Extractor API:
├── POST /api/extract     → Start extraction
├── GET /api/extract      → Get progress
└── GET /api/library      → Get extracted components
```

## Future Enhancements

### Design Extractor

- [ ] Component Detection (buttons, cards, modals)
- [ ] Spacing System extraction (gap, padding, margin)
- [ ] Interaction Patterns (hover, focus, transitions)
- [ ] Accessibility Analysis (ARIA, contrast)
- [ ] Responsive Breakpoints detection

### Library Extractor

- [ ] Multi-framework support (Vue, Svelte)
- [ ] Dependency graph generation
- [ ] Component documentation extraction
- [ ] StoryBook integration
