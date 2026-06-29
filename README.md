# Design Extractor Toolkit

> Unified toolkit for extracting design systems and components from live websites and GitHub repositories.


[![Next.js](https://img.shields.io/badge/Next.js-black?style=flat-square)](https://nextjs.org)
[![React](https://img.shields.io/badge/React-61DAFB?style=flat-square)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square)](https://www.typescriptlang.org)
[![Tailwind_CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square)](https://tailwindcss.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)


## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Architecture](#architecture)
- [Components](#components)
- [Quick Start](#quick-start)
- [Клонировать](#клонировать)
- [Установить зависимости](#установить-зависимости)
- [Запустить](#запустить)
- [Open http://localhost:3001](#open-http:localhost:3001)
- [Клонировать](#клонировать)
- [Использовать skill](#использовать-skill)
- [(интеграция через Z.ai Agent Toolkit)](#интеграция-через-zai-agent-toolkit)
- [Documentation](#documentation)
- [Templates](#templates)
- [Examples](#examples)
- [Related Projects](#related-projects)
- [Status](#status)
- [License](#license)

## Overview

**Design Extractor Toolkit** — это набор инструментов для реверс-инжиниринга UI дизайна:

- **Design Extractor** — извлекает design tokens с живых сайтов (URL)
- **Library Extractor** — извлекает React компоненты из GitHub репозиториев

## Features

- Feature 1 - description
- Feature 2 - description

## Tech Stack

- **Framework** - Next.js
- **Language** - TypeScript
- **Styling** - Tailwind CSS, CSS
- **Tools** - React

## Getting Started

### Prerequisites

- Node.js 20+ or Bun

### Installation

```bash
git clone https://github.com/stsgs1980/Design-extractor-toolkit.git
cd Design-extractor-toolkit
bun install
```

### Run

```bash
bun run dev
```

## Architecture

```bash
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
## Клонировать
gh repo clone Sts8987/reverse-engineering-svelte

## Установить зависимости
cd reverse-engineering-svelte
bun install
bunx playwright install chromium

## Запустить
bun run dev
## Open http://localhost:3001
```

### Library Extractor

```bash
## Клонировать
gh repo clone stsgs1980/zai-ui-kit

## Использовать skill
## (интеграция через Z.ai Agent Toolkit)
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
| Design Extractor | Production Ready | 2.0.0 |
| Library Extractor | In Development | 0.1.0 |

## License

MIT


**Maintained by:** @stsgs1980, @Sts8987

---
Built with: Next.js + React + TypeScript + Tailwind CSS
