# Lean Documentation Pipeline

## Overview

The lean documentation pipeline provides a streamlined path from idea to implementation-ready design, optimized for AI agent consumption and rapid development cycles.

## Pipeline Commands

### Individual Lean Commands

Each stage has both a standard (comprehensive) and lean (concise) version:

| Stage | Standard Command | Lean Command | Output Size |
|-------|-----------------|--------------|-------------|
| PRD | `/arch-toolkit:prd.create` | `/arch-toolkit:prd.create-lean` | 10-15 pages → 2-4 pages |
| Domain Model | `/arch-toolkit:ddd.create-model` | `/arch-toolkit:ddd.create-lean` | 8-12 pages → 2-3 pages |
| C4 Architecture | `/arch-toolkit:c4.create-model` | `/arch-toolkit:c4.create-lean` | 10-15 pages → 3-4 pages |
| Design Document | `/arch-toolkit:arch.create-design-document` | `/arch-toolkit:arch.create-design-lean` | 15-20 pages → 4-5 pages |

### Full Pipeline Commands

- **`/arch-toolkit:pipeline.full`** - Comprehensive documentation (50+ pages)
- **`/arch-toolkit:pipeline.lean`** - Lean documentation (~15 pages) ✨ NEW

## Lean vs Standard Comparison

### Lean Pipeline Characteristics

**Advantages:**
- 🚀 **90% faster generation** (2-3 minutes vs 20-30 minutes)
- 📄 **70% less content** (~15 pages vs 50+ pages)
- 🤖 **AI-optimized structure** for agent processing
- 🎯 **Implementation-focused** without theoretical background
- 🔄 **Iteration-friendly** for rapid changes

**Trade-offs:**
- Less detailed explanations
- Minimal background context
- Fewer examples
- No extensive rationale

### When to Use Lean Pipeline

**Perfect for:**
- Proof of concepts
- MVPs and prototypes
- Hackathons
- AI agent-driven development
- Rapid iteration cycles
- Small to medium projects
- Team already familiar with domain

**Use Standard Pipeline for:**
- Large enterprise projects
- Regulatory compliance needs
- Multi-team coordination
- Long-term maintenance projects
- Knowledge transfer requirements
- Complex architectural decisions
- Detailed documentation requirements

## Lean Document Structure

Each lean document follows a consistent pattern:

1. **Essential Information Only** - Core concepts without elaboration
2. **Bullet Points Over Paragraphs** - Quick scanning and parsing
3. **Code/Diagram Snippets** - Visual over verbal when possible
4. **Implementation Focus** - What to build, not why
5. **Clear Boundaries** - Explicit scope and non-scope
6. **Next Steps** - Clear path forward

## Usage Examples

### Generate Complete Lean Pipeline
```bash
/arch-toolkit:pipeline.lean "AI-powered code review tool for Python"
```

Creates:
```
lean-docs-[timestamp]/
├── README.md                    # Pipeline summary and navigation
├── 1-lean-prd.md               # Lean PRD (2-4 pages)
├── 2-lean-domain-model.md     # Lean Domain Model (2-3 pages)
├── 3-lean-c4-architecture.md  # Lean C4 Architecture (3-4 pages)
└── 4-lean-design-document.md  # Lean Design Document (4-5 pages)
```

### Generate Individual Lean Documents
```bash
# Start with lean PRD
/arch-toolkit:prd.create-lean "Task management for developers" tasks-prd.md

# Generate lean domain model from PRD
/arch-toolkit:ddd.create-lean tasks-prd.md tasks-domain.md

# Generate lean C4 architecture
/arch-toolkit:c4.create-lean tasks-prd.md tasks-domain.md tasks-c4.md

# Generate lean design document
/arch-toolkit:arch.create-design-lean tasks-prd.md tasks-domain.md tasks-c4.md tasks-design.md
```

## Integration with Development Workflow

### Typical Lean Workflow

1. **Ideation** → `/arch-toolkit:pipeline.lean "idea"`
2. **Review** → Quick team review of lean docs (30 min)
3. **Implementation** → `/arch-toolkit:dev.implement-feature` using lean design doc
4. **Iteration** → Regenerate specific docs as needed
5. **Expansion** → Generate standard docs for specific areas if needed

### Mixing Lean and Standard

You can mix approaches:
- Start with lean pipeline for speed
- Expand specific documents to standard version later
- Use lean for exploration, standard for final documentation

Example:
```bash
# Start with lean pipeline
/arch-toolkit:pipeline.lean "New feature idea"

# Later, expand domain model to full version
/arch-toolkit:ddd.create-model lean-docs/1-lean-prd.md full-domain-model.md

# Or expand C4 for detailed architecture review
/arch-toolkit:c4.create-model lean-docs/1-lean-prd.md full-domain-model.md detailed-c4.md
```

## Best Practices

1. **Start Lean** - Begin with lean pipeline for new projects
2. **Iterate Quickly** - Regenerate lean docs as requirements evolve
3. **Expand Selectively** - Only create detailed docs where needed
4. **Keep Both** - Lean for development, standard for documentation
5. **Review Regularly** - Lean docs should be living documents

## Performance Metrics

Typical generation times:

| Pipeline Type | Total Time | Total Pages | Words |
|--------------|------------|-------------|--------|
| Lean Pipeline | 2-3 min | ~15 pages | ~3,000 |
| Standard Pipeline | 20-30 min | 50+ pages | ~12,000 |

## Future Enhancements

Potential additions to lean pipeline:
- `/test.create-lean` - Lean test strategy
- `/api.create-lean` - Lean API specification
- `/deploy.create-lean` - Lean deployment plan
- `/security.create-lean` - Lean security checklist

---

The lean pipeline represents a paradigm shift in documentation: from comprehensive to sufficient, from exhaustive to actionable, from human-centric to AI-optimized.