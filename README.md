# Design Extractor Toolkit

Unified toolkit for extracting design systems and components from live websites and GitHub repositories. Includes a Design Extractor (from URL via SvelteKit + Playwright) and a Library Extractor (from GitHub repo via Z.ai Agent Toolkit), both feeding into a central UI-Kit Studio control center.

[![Next.js](https://img.shields.io/badge/Next.js-black?style=flat-square)](https://nextjs.org)
[![React](https://img.shields.io/badge/React-61DAFB?style=flat-square)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square)](https://www.typescriptlang.org)
[![Tailwind_CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square)](https://tailwindcss.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

## Features

- Design Extractor: extracts tech stack (framework, CSS, analytics), design tokens (colors, typography, spacing), screenshots (full page, sections, responsive), and CSS variables/animations from live websites via URL
- Library Extractor: extracts React/Next.js components, custom hooks, utility functions, TypeScript types, and token systems from GitHub repositories
- Two extraction pipelines (URL-based and repo-based) converging into UI-Kit Studio as the central control center
- Design Extractor built with SvelteKit 2.x + Playwright + Tailwind CSS 4
- Library Extractor integrates with Z.ai Agent Toolkit
- Architecture documentation with component-level diagrams

## Tech Stack

- **Design Extractor** - SvelteKit 2.x + Playwright + Tailwind CSS 4
- **Library Extractor** - Z.ai Agent Toolkit
- **Toolkit Hub** - Next.js + TypeScript + Tailwind CSS

## Getting Started

### Prerequisites

- Bun
- Playwright (for Design Extractor)

### Installation

**Design Extractor:**

```bash
gh repo clone Sts8987/reverse-engineering-svelte
cd reverse-engineering-svelte
bun install
bunx playwright install chromium
```

**Library Extractor:**

```bash
gh repo clone stsgs1980/zai-ui-kit
```

### Run

**Design Extractor:**

```bash
bun run dev
```

Open http://localhost:3001

**Library Extractor:** Use through Z.ai Agent Toolkit integration.

## Architecture

```text
+-------------------------------------------------------------+
|                    Design Extractor Toolkit                  |
+-------------------------------------------------------------+
|                                                             |
|   +---------------------+   +-----------------------------+|
|   |   Design Extractor  |   |    Library Extractor        ||
|   |   (from URL)        |   |    (from GitHub repo)       ||
|   |                     |   |                             ||
|   |   INPUT: URL        |   |   INPUT: GitHub repo URL    ||
|   |   OUTPUT:           |   |   OUTPUT:                   ||
|   |   - Design tokens   |   |   - React components        ||
|   |   - Tech stack      |   |   - Hooks                   ||
|   |   - Screenshots     |   |   - Utils                   ||
|   |   - CSS variables   |   |   - Types                   ||
|   +----------+----------+   +--------------+--------------+|
|              |                             |                |
|              +----------+------------------+                |
|                         |                                   |
|                         v                                   |
|              +---------------------+                        |
|              |   UI-Kit Studio     |                        |
|              |   (Control Center)  |                        |
|              +---------------------+                        |
|                                                             |
+-------------------------------------------------------------+
```

## Status

| Component | Status | Version |
|-----------|--------|---------|
| Design Extractor | Production Ready | 2.0.0 |
| Library Extractor | In Development | 0.1.0 |

## Documentation

- [Architecture Overview](docs/architecture.md)
- [Design Extractor Guide](docs/design-extractor.md)
- [Library Extractor Guide](docs/library-extractor.md)
- [Integration with UI-Kit](docs/integration.md)

## Related Projects

| Project | Purpose | Link |
|---------|---------|------|
| **UI-Kit** | Interface Studio (Control Center) | `stsgs1980/UI-Kit` |
| **zai-ui-kit** | Component Library + Library Extractor | `stsgs1980/zai-ui-kit` |
| **reverse-engineering-svelte** | Design Extractor Engine | `Sts8987/reverse-engineering-svelte` |

## License

MIT

**Maintained by:** @stsgs1980, @Sts8987

---
Built with: Next.js + SvelteKit + TypeScript + Tailwind CSS