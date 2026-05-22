# Design Extractor Toolkit

> Unified toolkit for extracting design systems and components from live websites and GitHub repositories.

## Overview

**Design Extractor Toolkit** — это набор инструментов для реверс-инжиниринга UI дизайна:

- **Design Extractor** — извлекает design tokens с живых сайтов (URL)
- **Library Extractor** — извлекает React компоненты из GitHub репозиториев

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Design Extractor Toolkit                 │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   ┌─────────────────────┐   ┌─────────────────────────────┐│
│   │   Design Extractor  │   │    Library Extractor        ││
│   │   (from URL)        │   │    (from GitHub repo)       ││
│   │                     │   │                             ││
│   │   INPUT: URL        │   │   INPUT: GitHub repo URL    ││
│   │   OUTPUT:           │   │   OUTPUT:                   ││
│   │   - Design tokens   │   │   - React components        ││
│   │   - Tech stack      │   │   - Hooks                   ││
│   │   - Screenshots     │   │   - Utils                   ││
│   │   - CSS variables   │   │   - Types                   ││
│   └──────────┬──────────┘   └──────────────┬──────────────┘│
│              │                             │                │
│              └──────────┬──────────────────┘                │
│                         │                                   │
│                         ▼                                   │
│              ┌─────────────────────┐                        │
│              │   UI-Kit Studio     │                        │
│              │   (Control Center)  │                        │
│              └─────────────────────┘                        │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## Components

### 1. Design Extractor (from URL)

**Репозиторий:** `Sts8987/reverse-engineering-svelte`

Извлекает design system с живых сайтов:
- Tech Stack (framework, CSS, analytics)
- Design Tokens (colors, typography, spacing)
- Screenshots (full page, sections, responsive)
- CSS Variables & Animations

**Стек:** SvelteKit 2.x + Playwright + Tailwind CSS 4

### 2. Library Extractor (from GitHub repo)

**Репозиторий:** `stsgs1980/zai-ui-kit`

Извлекает компоненты из GitHub репозиториев:
- React/Next.js компоненты
- Custom hooks
- Utility functions
- TypeScript types
- Token systems

## Quick Start

### Design Extractor

```bash
# Клонировать
gh repo clone Sts8987/reverse-engineering-svelte

# Установить зависимости
cd reverse-engineering-svelte
bun install
bunx playwright install chromium

# Запустить
bun run dev
# Open http://localhost:3001
```

### Library Extractor

```bash
# Клонировать
gh repo clone stsgs1980/zai-ui-kit

# Использовать skill
# (интеграция через Z.ai Agent Toolkit)
```

## Documentation

- [Architecture Overview](docs/architecture.md)
- [Design Extractor Guide](docs/design-extractor.md)
- [Library Extractor Guide](docs/library-extractor.md)
- [Integration with UI-Kit](docs/integration.md)

## Templates

- [Library Extractor Template](templates/library-extractor/template.json)
- [Design Extractor Template](templates/design-extractor/template.json)

## Examples

- [Example Output](examples/example-output.json) — пример извлечённой дизайн-системы

## Related Projects

| Project | Purpose | Link |
|---------|---------|------|
| **UI-Kit** | Interface Studio (Control Center) | `stsgs1980/UI-Kit` |
| **zai-ui-kit** | Component Library + Library Extractor | `stsgs1980/zai-ui-kit` |
| **reverse-engineering-svelte** | Design Extractor Engine | `Sts8987/reverse-engineering-svelte` |

## Status

| Component | Status | Version |
|-----------|--------|---------|
| Design Extractor | ✅ Production Ready | 2.0.0 |
| Library Extractor | 🚧 In Development | 0.1.0 |

## License

MIT

---

**Maintained by:** @stsgs1980, @Sts8987
