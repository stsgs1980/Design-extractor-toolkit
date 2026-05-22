# Library Extractor Guide

> Extract React components, hooks, and utilities from GitHub repositories.

## Overview

**Library Extractor** анализирует GitHub репозитории и извлекает:

- React/Next.js компоненты
- Custom hooks
- Utility functions
- TypeScript types
- Token systems

## Repository

```
GitHub: https://github.com/stsgs1980/zai-ui-kit
Status: In Development (v0.1.0)
```

## Tech Stack

| Technology | Purpose |
|------------|---------|
| TypeScript | Implementation |
| AST Parser | Code analysis |
| Z.ai Skill | Integration |

## Architecture

### Extraction Pipeline

```
┌─────────────────────────────────────────────────────────────┐
│                 Library Extractor Pipeline                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  INPUT: GitHub Repository URL                               │
│         https://github.com/user/repo                        │
│                                                             │
│  Phase 1: Repository Scan                                   │
│  ├── Clone repository                                       │
│  ├── Parse file structure                                   │
│  ├── Identify tech stack (React, Vue, Svelte)              │
│  └── Detect component locations                             │
│                                                             │
│  Phase 2: Component Detection                               │
│  ├── React components (.tsx, .jsx)                         │
│  ├── Vue components (.vue)                                  │
│  ├── Svelte components (.svelte)                           │
│  └── Web components                                         │
│                                                             │
│  Phase 3: Extraction                                        │
│  ├── Component code                                         │
│  ├── Dependencies (imports)                                 │
│  ├── Props interfaces                                       │
│  ├── Hooks used                                             │
│  └── Styles (CSS, Tailwind classes)                        │
│                                                             │
│  Phase 4: Classification                                    │
│  ├── UI components (Button, Card, Modal...)                │
│  ├── Hooks (useAuth, useLocalStorage...)                   │
│  ├── Utils (formatDate, cn...)                             │
│  ├── Types (interfaces, types)                              │
│  └── Tokens (colors, spacing, typography)                   │
│                                                             │
│  Phase 5: Package Generation                                │
│  ├── package.json                                           │
│  ├── index.ts (exports)                                     │
│  ├── TypeScript definitions                                 │
│  └── README.md                                              │
│                                                             │
│  OUTPUT: npm package / Component Library                    │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## Component Categories

### Atomic Design Structure

```
components/
├── tokens/           # Design tokens
│   ├── colors.ts
│   ├── spacing.ts
│   └── typography.ts
│
├── ui/               # Base UI components
│   ├── Button.tsx
│   ├── Card.tsx
│   ├── Input.tsx
│   └── Modal.tsx
│
├── sections/         # Page sections
│   ├── Hero.tsx
│   ├── Navbar.tsx
│   └── Footer.tsx
│
├── features/         # Feature components
│   ├── SearchBar.tsx
│   └── UserMenu.tsx
│
├── hooks/            # Custom hooks
│   ├── useAuth.ts
│   └── useLocalStorage.ts
│
└── providers/        # Context providers
    └── ThemeProvider.tsx
```

## Detection Patterns

### React Components

```typescript
// Detection criteria
const patterns = {
  // File extensions
  extensions: ['.tsx', '.jsx'],

  // Component patterns
  componentPatterns: [
    'export function Component',
    'export const Component',
    'export default function',
    'const Component = () =>',
    'function Component('
  ],

  // Props patterns
  propsPatterns: [
    'interface Props',
    'type Props',
    '{ }: Props'
  ]
};
```

### Hooks

```typescript
const hookPatterns = {
  // File naming
  filePattern: /^use[A-Z]/,

  // Function pattern
  exportPattern: 'export function use',
  constPattern: 'export const use'
};
```

### Utils

```typescript
const utilPatterns = {
  // Common utility files
  files: ['utils.ts', 'helpers.ts', 'lib.ts'],

  // Common utilities
  functions: ['cn', 'formatDate', 'debounce', 'throttle']
};
```

## Output Format

### Component JSON

```json
{
  "name": "Button",
  "file": "src/components/ui/Button.tsx",
  "type": "ui",
  "props": [
    { "name": "variant", "type": "'primary' | 'outline'", "default": "'primary'" },
    { "name": "size", "type": "'sm' | 'md' | 'lg'", "default": "'md'" },
    { "name": "children", "type": "ReactNode", "required": true }
  ],
  "imports": [
    "react",
    "class-variance-authority",
    "./button.styles"
  ],
  "exports": ["Button", "buttonVariants"],
  "dependencies": {
    "react": "^18.0.0",
    "class-variance-authority": "^0.7.0"
  },
  "lines": 85,
  "complexity": "low"
}
```

### Library Package

```
@extracted/library-name/
├── package.json
├── index.ts
├── components/
│   ├── ui/
│   ├── sections/
│   └── features/
├── hooks/
├── utils/
├── types/
└── tokens/
```

## Usage

### Via Z.ai Skill

```
Use Library Extractor skill to extract components from:
https://github.com/user/repo-name
```

### Via API (Planned)

```bash
# Start extraction
curl -X POST http://localhost:3000/api/extract \
  -H "Content-Type: application/json" \
  -d '{"repo": "https://github.com/user/repo"}'

# Check progress
curl "http://localhost:3000/api/extract?job=123"

# Get results
curl http://localhost:3000/api/library
```

## Configuration

### Template

See [template.json](../templates/library-extractor/template.json)

```json
{
  "source": {
    "repo": "https://github.com/user/repo",
    "branch": "main",
    "paths": ["src/components", "src/lib"]
  },
  "extraction": {
    "components": true,
    "hooks": true,
    "utils": true,
    "types": true,
    "tokens": true
  },
  "output": {
    "format": "npm-package",
    "name": "@extracted/library",
    "includeStyles": true
  }
}
```

## Integration with UI-Kit

Library Extractor интегрируется с UI-Kit Studio:

```
UI-Kit Studio
│
├── /extractor
│   └── Library Extractor Dashboard
│       ├── Input: GitHub URL
│       ├── Progress: Extraction status
│       └── Output: Component library
│
└── /library
    └── Extracted Components
        ├── Browse
        ├── Preview
        └── Use in Studio
```

## Current Status

| Feature | Status |
|---------|--------|
| Repository Clone | ✅ Ready |
| File Structure Scan | ✅ Ready |
| React Component Detection | 🚧 In Progress |
| Hook Extraction | 📋 Planned |
| Utils Extraction | 📋 Planned |
| Package Generation | 📋 Planned |

## Related Documentation

- [Architecture Overview](architecture.md)
- [Design Extractor Guide](design-extractor.md)
- [Template](../templates/library-extractor/template.json)
