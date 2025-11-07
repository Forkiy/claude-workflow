# Software Architecture Toolkit - Claude Code Plugin

A comprehensive Claude Code plugin providing specialized agents and commands for professional software architecture, design, and development workflows.

## Features

### Specialized Agents

- **Bob Martin Architect** - Clean architecture and SOLID principles expert
- **Kent Beck Implementer** - TDD and practical implementation expert
- **Jeff Patton PM** - User story mapping and epic decomposition expert
- **DDD Architect** - Domain-Driven Design specialist
- **C4 Architecture Advisor** - C4 model and architecture documentation expert
- **Ken Norton PRD Expert** - Product Requirements Document specialist

### Command Categories

#### Product & Requirements (`/prd:*`)
- `/prd:create` - Create comprehensive PRD using Ken Norton's methodology
- `/prd:create-lean` - Create lean, engineering-focused PRD (2-4 pages)

#### Domain-Driven Design (`/ddd:*`)
- `/ddd:create-model` - Create domain model from PRD
- `/ddd:create-lean` - Create lean domain model (2-3 pages)
- `/ddd:extract-model` - Extract domain model from existing codebase
- `/ddd:review-model` - Review domain model for DDD alignment

#### Architecture (`/arch:*`)
- `/arch:create-design-document` - Create architectural design from PRD
- `/arch:create-design-lean` - Create lean design document (4-5 pages)
- `/arch:review` - Review existing architecture with Bob Martin's expertise
- `/arch:code-review` - Review code for clean code principles
- `/arch:audit` - Comprehensive architecture audit with metrics
- `/arch:verify-implementation` - Verify implementation against design
- `/arch:evaluate-idea` - Evaluate architectural changes or ideas
- `/arch:create-context-file` - Create comprehensive technical reference

#### C4 Architecture (`/c4:*`)
- `/c4:create-model` - Create C4 diagrams from PRD and domain model
- `/c4:create-lean` - Create lean C4 model (3-4 pages)
- `/c4:review-architecture` - Review architecture documentation

#### Development (`/dev:*`)
- `/dev:implement-tdd` - Implement features using strict TDD
- `/dev:implement-feature` - Start implementing from design document
- `/dev:fix-bug` - Fix bugs with TDD approach (test first)
- `/dev:refactor-tdd` - Refactor code while maintaining tests

#### Project Management (`/pm:*`)
- `/pm:decompose-epics` - Decompose design into user story epics
- `/pm:validate-epics` - Validate epic decomposition
- `/pm:story-mapping` - Facilitate interactive story mapping workshop
- `/pm:roadmap` - Create implementation roadmap with milestones

#### Pipeline (`/pipeline:*`)
- `/pipeline:full` - Execute complete pipeline from PRD to implementation
- `/pipeline:lean` - Execute lean document pipeline (PRD → Domain → C4 → Design)
- `/pipeline:run` - Orchestrate pipeline with intelligent stage management

#### Git Workflows (`/git:*`)
- `/git:commit` - Create commits following repository conventions
- `/git:merge` - Squash and merge branch to main

## Installation

### From GitHub

```bash
# Add the GitHub repository as a marketplace
/plugin marketplace add https://github.com/Forkiy/claude-workflow.git

# Install the plugin
/plugin install arch-toolkit
```

### Via Settings File

Add to your `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": [
    {
      "source": "https://github.com/Forkiy/claude-workflow.git"
    }
  ],
  "plugins": [
    "arch-toolkit"
  ]
}
```

### For Local Development

```bash
# Add local marketplace
/plugin marketplace add /Users/forkiy/Work/claude-workflow

# Install plugin
/plugin install arch-toolkit
```

## Usage Examples

### Full Development Pipeline

```bash
# Create complete documentation pipeline
/pipeline:lean "Build a task management API"

# Implement from design
/dev:implement-tdd design.md
```

### Architecture Review

```bash
# Review existing architecture
/arch:review

# Audit with metrics
/arch:audit
```

### Feature Development

```bash
# Start new feature
/dev:implement-feature feature-spec.md

# Fix bug with TDD
/dev:fix-bug "User login fails with special characters"
```

## Documentation Pipeline

The plugin supports progressive refinement workflows:

1. **PRD** (Product Requirements) → Business requirements
2. **Domain Model** → Core business concepts
3. **C4 Architecture** → System structure
4. **Design Document** → Implementation blueprint
5. **Implementation** → TDD-driven code

## License

MIT

## Support

For issues and questions, please use the repository issue tracker.
