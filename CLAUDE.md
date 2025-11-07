# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Claude Code plugin repository providing a comprehensive software architecture and development toolkit. The plugin contains 40+ specialized commands and 6 expert agents that implement professional methodologies from renowned architects and product managers (Bob Martin, Kent Beck, Jeff Patton, Vaughn Vernon, Simon Brown, Ken Norton).

## Core Architecture

### Command-Agent Separation Pattern

**CRITICAL:** This codebase follows a strict separation of concerns:

**Commands** (`/commands/[category]/`) handle:
- Parsing arguments from `$ARGUMENTS` variable
- File I/O operations (reading inputs, writing outputs)
- Orchestrating workflows (what needs to be done)
- Launching agents via Task tool

**Agents** (`/agents/`) provide:
- Domain expertise and methodologies
- Personality and decision-making logic
- Implementation of how tasks are accomplished
- Consistent approach across invocations

### Command Structure

Every command follows this pattern:
```yaml
---
allowed-tools: Task, Read, Write, Glob    # Tool restrictions for safety
argument-hint: <required> [optional]      # User guidance
description: Brief description             # Help text
---
```

The markdown body contains the workflow logic that:
1. Parses arguments
2. Reads necessary files
3. Launches appropriate agents with full context
4. Processes results (save or display)

### Agent Invocation Pattern

Commands MUST invoke agents with complete context in a single prompt (agents are stateless):
```markdown
Use the Task tool to launch the [agent-name] agent:

"You are operating in [MODE] - [context description]"
[Detailed task instructions]

**INPUT FILES:**
- File path: [FULL PATH]

**OUTPUT REQUIREMENTS:**
1. Use Write tool to save files
2. Return only brief summary
3. DO NOT read back saved files
```

## Document Generation Pipeline

The architecture follows a progressive refinement workflow:
```
PRD → Domain Model → C4 Architecture → Design Document → Implementation
```

Each stage builds on the previous with two variants:
- **Full**: Comprehensive documentation (50+ pages total)
- **Lean**: AI-optimized, implementation-focused (15 pages total)

## Common Commands

### Development Workflow
```bash
# Start new feature with TDD implementation
/arch-toolkit:dev.implement-tdd <design-doc.md> [output-dir]

# Fix a bug (enforces test-first approach)
/arch-toolkit:dev.fix-bug <bug-description>

# Refactor with TDD safety net
/arch-toolkit:dev.refactor-tdd <file-or-directory>
```

### Pipeline Commands
```bash
# Execute full pipeline from idea to implementation
/arch-toolkit:pipeline.lean "Build a task management API"

# Run specific pipeline stages
/arch-toolkit:pipeline.run <stage> <input-files>
```

### Architecture Commands
```bash
# Comprehensive architecture review with Bob Martin
/arch-toolkit:arch.review [directory]

# Audit codebase with metrics
/arch-toolkit:arch.audit

# Verify implementation matches design
/arch-toolkit:arch.verify-implementation <design-doc> <implementation-dir>

# Evaluate architectural changes
/arch-toolkit:arch.evaluate-idea "Split payment service into microservice"
```

### Git Operations
```bash
# Create semantic commits
/arch-toolkit:git.commit [prefix]

# Squash and merge to main
/arch-toolkit:git.merge
```

### Product & Design Commands
```bash
# Create lean PRD (AI-optimized)
/arch-toolkit:prd.create-lean <project-idea> [output]

# Create domain model from PRD
/arch-toolkit:ddd.create-model <prd-file> [output]

# Create C4 architecture diagrams
/arch-toolkit:c4.create-lean <prd> <domain-model> [output]

# Decompose into epics
/arch-toolkit:pm.decompose-epics <design-doc> [output]
```

## Key Patterns & Conventions

### Multi-File Document Structure
Complex documents are split into hierarchical structures:
```
main-document.md (navigation hub, 100-300 lines)
main-document/
  ├── section-1.md (focused content)
  ├── section-2.md (natural boundaries)
  └── section-3.md (~300-400 line threshold)
```

### Output Policy
Agents follow strict constraints:
1. Save files directly using Write tool (never in response)
2. Return brief summary only (5-20 lines)
3. NO full document content in responses
4. NO reading back saved files

### Code in Design Documents
**FORBIDDEN:**
- Complete function implementations
- Detailed algorithms
- Copy-pasteable code

**ACCEPTABLE:**
- Interface definitions (5-10 lines max)
- High-level pseudocode
- API contracts
- PlantUML diagrams (preferred)

### File Naming Conventions
- Commands: `/[category]/[verb]-[noun].md` (kebab-case)
- Agents: `[firstname]-[lastname]-[role].md`
- Outputs: User-specified or semantic defaults

## Testing & Validation

While there are no automated tests in this repository (it's a command/agent plugin), the architecture enforces quality through:
- TDD-first development commands (`/arch-toolkit:dev.implement-tdd`, `/arch-toolkit:dev.fix-bug`)
- Design verification (`/arch-toolkit:arch.verify-implementation`)
- Epic validation (`/arch-toolkit:pm.validate-epics`)
- Architecture reviews (`/arch-toolkit:arch.review`, `/arch-toolkit:arch.audit`)

## Local Development

### Running Commands Directly
Commands can be tested by:
1. Reading the command file to understand allowed tools and arguments
2. Using the SlashCommand tool: `SlashCommand("/command-name arguments")`
3. Checking output files for results

### Modifying Commands
When editing commands:
- Maintain YAML frontmatter structure
- Respect allowed-tools restrictions
- Follow the command-agent separation pattern
- Test with various argument combinations

### Adding New Commands
1. Create file in appropriate `/commands/[category]/` folder
2. Add YAML frontmatter with allowed-tools, argument-hint, description
3. Follow existing patterns for agent invocation
4. Update marketplace.json if needed

### Adding New Agents
1. Create markdown file in `/agents/` directory
2. Add YAML frontmatter with name, description, color, model
3. Define clear personality and methodology
4. Ensure stateless operation (full context in single prompt)

## Architecture Principles

1. **Trust Expert Agents**: Commands provide context; agents make decisions independently
2. **Document Hierarchies**: Complex systems get multiple documents with clear navigation
3. **File-Based Workflow**: Code stays in files, not conversation
4. **Progressive Refinement**: Each pipeline stage builds on previous work
5. **Pragmatic Over Perfect**: Usable documents beat academic purity
6. **Diagram First**: Visual communication (PlantUML) replaces verbose text

## Integration Notes

### Plugin Installation
```bash
# For local development
/plugin marketplace add /Users/forkiy/Work/claude-workflow
/plugin install software-architecture-toolkit
```

### Command Discovery
- Use `/help` to see all available commands
- Commands are organized by category (prd, ddd, arch, c4, dev, pm, pipeline, git)
- Each command has a description in its frontmatter

### Model Preferences
- Default: Standard operations (claude-3.5-sonnet)
- Haiku: Fast operations (git commits)
- Opus: Complex analysis (comprehensive audits)