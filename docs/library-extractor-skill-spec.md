# Library Extractor Skill Specification

> **Status:** Draft
> **Created:** 2025-01-16
> **Purpose:** Extract reusable components from N projects → Component Library + Interactive Playground

---

## Overview

```
📁 N проектов → 🔍 Анализ → 📦 Библиотека компонентов → 📚 Docs + Playground
```

**Goal:** Transform 40+ user projects into a unified, reusable component library with 21st.dev-style interactive documentation.

---

## Skill Structure

```
library-extractor/
├── SKILL.md                    # Main instruction file
├── config/
│   ├── defaults.yaml           # Default settings
│   └── atomic-design.yaml      # Classification rules
├── prompts/
│   ├── 01-index.md             # Prompt: Project indexing
│   ├── 02-analyze.md           # Prompt: Code analysis
│   ├── 03-extract.md           # Prompt: Extraction
│   ├── 04-enrich.md            # Prompt: Metadata enrichment
│   └── 05-output.md            # Prompt: Output generation
├── templates/
│   ├── component-library/      # Library structure template
│   └── playground.html         # Interactive playground template
└── examples/
    └── energy-helix-3d/        # Working example
```

---

## Pipeline (5 Stages)

### Stage 1: Index

**Goal:** Scan project and understand structure

**LLM Task:**
- Find all source files
- Identify file types (components, utils, types, styles)
- Build dependency graph
- Detect framework (React, Vue, Next.js, etc.)

**Output:** `project-index.json`

---

### Stage 2: Analyze

**Goal:** Identify reusable code units

**LLM Task:**
- Parse components → props, state, dependencies
- Parse functions → purity, inputs, outputs
- Parse types → interfaces, type aliases
- Classify by Atomic Design (atoms, molecules, organisms)

**Output:** `analysis-report.json`

---

### Stage 3: Extract

**Goal:** Extract reusable code

**LLM Task:**
- Copy component code
- Resolve dependencies
- Remove business logic (optional)
- Normalize imports

**Output:** Extracted code files

---

### Stage 4: Enrich

**Goal:** Add metadata for each extracted item

**LLM Task:**
- Calculate reusability score
- Identify dependencies
- Add source traceability
- Generate usage examples

**Output:** Enriched metadata

---

### Stage 5: Output

**Goal:** Generate final deliverables

**LLM Task:**
- Create npm-package structure
- Generate playground.html
- Create README.md
- Create extraction-report.json

**Output:** Complete component library

---

## Classification Rules (Atomic Design)

### Atoms (highest reusability)

```yaml
criteria:
  - Pure functions (no side effects)
  - TypeScript types/interfaces
  - CSS utilities
  - Constants
  - Basic UI primitives (buttons, inputs, icons)
  - Hooks with no business logic

examples:
  - calculateHelixPosition()
  - TorusRing geometry
  - HelixPoint interface
  - formatCurrency()
```

### Molecules (medium reusability)

```yaml
criteria:
  - React components (presentational)
  - Custom hooks with simple logic
  - Small compositions (2-3 atoms)
  - Form fields with validation
  - Cards, modals, dropdowns

examples:
  - BuyerNodes (instancedMesh + interaction)
  - SelectionRing (torus + glow + animation)
  - VolumeHeatmap
```

### Organisms (lower reusability)

```yaml
criteria:
  - Complex components
  - Business logic containers
  - Page sections
  - Data providers
  - Feature compositions

examples:
  - SpiralBackbone (full helix structure)
  - NodeSystem (buyers + sellers + selection)
  - EnergyHelix (root orchestrator)
```

---

## Reusability Score Algorithm

```yaml
base_score: 50

positive_factors:
  - pure_function: +30
  - typescript_typed: +10
  - has_tests: +15
  - props_count: +5 per prop (configurable)
  - zero_dependencies: +20
  - documented: +10

negative_factors:
  - business_logic: -20
  - external_dependencies: -5 per dep
  - lines_over_50: -1 per 10 lines
  - hardcoded_values: -10
  - domain_specific: -15

formula: |
  score = base_score
        + sum(positive_factors)
        - sum(negative_factors)
  score = max(0, min(100, score))
```

---

## Source Traceability

Every extracted component must reference its source:

```json
{
  "id": "torus-ring",
  "name": "TorusRing",
  "type": "atom",
  "reusabilityScore": 98,
  "source": {
    "project": "energy-helix-3d",
    "repository": "https://github.com/stsgs1980/energy-helix-3d",
    "file": "src/Backbone.tsx",
    "lines": [23, 35],
    "commit": "a1b2c3d",
    "extractedAt": "2025-01-16T10:30:00Z"
  }
}
```

---

## Output Formats

### 1. Component Library (npm package)

```
component-library/
├── package.json
├── src/
│   ├── index.ts
│   ├── atoms/
│   │   ├── TorusRing.tsx
│   │   ├── PulsingCore.tsx
│   │   └── ...
│   ├── molecules/
│   │   ├── BuyerNodes.tsx
│   │   └── ...
│   ├── organisms/
│   │   └── ...
│   ├── types/
│   │   └── index.ts
│   └── utils/
│       └── helixMath.ts
├── README.md
└── playground.html
```

### 2. Interactive Playground (HTML)

Features:
- Component selector (atoms, molecules, organisms)
- Live preview (CSS animation placeholder / iframe)
- Code viewer with syntax highlighting
- Props editor (sliders, color pickers, toggles)
- Generated usage code
- Copy to clipboard

Reference: `energy-helix-3d/examples/reference-guide.html` (Extracted tab)

### 3. Extraction Report (JSON)

```json
{
  "version": "1.0.0",
  "extractedAt": "2025-01-16T10:30:00Z",
  "sourceProjects": 3,
  "summary": {
    "atoms": 12,
    "molecules": 6,
    "organisms": 4,
    "avgReusability": 85
  },
  "components": [...]
}
```

---

## Configuration Options

```yaml
# defaults.yaml
extraction:
  input:
    - /path/to/project1
    - /path/to/project2

  output:
    library: ./component-library
    playground: ./playground.html
    report: ./extraction-report.json

  filters:
    includePatterns:
      - "src/**/*.{ts,tsx}"
      - "components/**/*"
    excludePatterns:
      - "**/*.test.{ts,tsx}"
      - "**/*.stories.{ts,tsx}"
      - "**/node_modules/**"

  scoring:
    reusabilityThreshold: 50  # minimum score to extract

  playground:
    theme: dark
    showSourceLink: true
    enableCodeEditor: true
```

---

## Example Usage (Future)

```bash
# CLI usage
library-extractor extract ./projects/* --output ./my-library

# With config
library-extractor extract --config ./extractor-config.yaml

# Dry run (analysis only)
library-extractor analyze ./project --dry-run
```

---

## Dependencies

- **LLM** for code analysis and extraction
- **AST Parser** for code parsing (optional, enhances accuracy)
- **File System** access for reading/writing
- **Package Manager** for dependency resolution

---

## Success Metrics

| Metric | Target |
|--------|--------|
| Extraction accuracy | >90% |
| False positives | <10% |
| Reusability score correlation | >0.8 |
| Playground load time | <2s |
| Components per project | 5-20 avg |

---

## Next Steps

1. Create `SKILL.md` with full instructions
2. Create prompt templates for each stage
3. Test on energy-helix-3d (already has reference)
4. Test on 2+ user projects
5. Iterate on classification rules
6. Build interactive playground generator

---

## References

- Atomic Design: https://atomicdesign.bradfrost.com/
- 21st.dev: https://21st.dev/ (inspiration)
- Storybook: https://storybook.js.org/ (similar concept)
- Current demo: `energy-helix-3d/examples/reference-guide.html`
