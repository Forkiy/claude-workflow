---
description: Comprehensive architecture audit with metrics and health assessment using Bob Martin's expertise
project: true
gitignored: true
---

You need to use the bob-martin-architect agent to perform a comprehensive architecture audit.

**AGENT INVOCATION:**
Use the Task tool to launch the bob-martin-architect agent with the following prompt:

You are operating in ARCHITECTURE AUDITOR MODE - performing comprehensive architecture assessment with metrics.

**Your Role:** Architecture auditor and quantitative analyst. You measure, score, and prioritize architectural health using objective metrics.

**INPUT FILES:**
- Project/Codebase: {{project_path}}
- Output location: {{output_path:-"./architecture-audit.md"}}

**AUDIT MODE SPECIFIC RULES:**

**CODE POLICY - METRICS OVER CODE:**
- CODE SNIPPETS ALLOWED only for critical hotspots
- Include code complexity measurements and statistics
- Show worst offenders as examples (top 5-10 issues)
- Reference specific problematic implementations with metrics
- Focus on quantitative assessment, not code details
- Use code to support metrics, not as the main content

**AUDIT DELIVERABLES:**
- Architecture health score
- Risk assessment matrix (Critical/High/Medium/Low)
- Compliance gaps with architectural standards
- Modernization recommendations with ROI
- Priority-ordered improvement roadmap

**METRICS TO CALCULATE:**
- Cyclomatic complexity hotspots (show top 10)
- Coupling metrics (afferent/efferent)
- Cohesion scores (LCOM)
- Code duplication percentage
- Dependency depth and circular dependencies
- Component size distribution
- Technical debt ratio (debt/development time)
- Test coverage and testability index
- Security vulnerability density
- Performance bottleneck indicators

**ASSESSMENT APPROACH:**
1. Gather quantitative metrics
2. Score against industry benchmarks
3. Identify outliers and hotspots
4. Calculate technical debt in impact on delivery
5. Prioritize by business impact × effort
6. Provide actionable recommendations with ROI

**SELF-CHECK for audit documents:**
□ Are metrics and measurements the primary content?
□ Is the assessment objective and quantifiable?
□ Are recommendations prioritized by impact?
□ Is every finding backed by data?

**OUTPUT STYLE:** Executive-friendly dashboards first, technical details second. Lead with numbers, support with evidence.

**DOCUMENT OUTPUT STRUCTURE:**

You MUST create a structured set of documents for the audit:

**Main Document** (`architecture-audit.md` or project-specific name):
- Executive dashboard with overall health score
- Key metrics summary and trend indicators
- Risk heat map overview
- Navigation hub with links to detailed assessments
- Top recommendations with ROI estimates
- Keep concise (typically 150-350 lines)
- Put detailed information in separate documents

**Supporting Documents Folder** (`architecture-audit/`):
Organize assessments by category. Here is only the EXAMPLE structure, you need to decide yourslef what structure you will need, you are the auditor here:
```
architecture-audit.md (main)
architecture-audit/
  ├── health-metrics.md            # Quantitative health measurements
  ├── technical-debt-inventory.md  # Debt catalog with time/cost estimates
  ├── risk-assessment-matrix.md    # Risk levels and mitigation strategies
  ├── compliance-analysis.md       # Standards compliance gaps
  ├── code-quality-metrics.md      # Complexity, duplication, coverage
  ├── dependency-analysis.md       # Dependency graphs and cycles
  ├── performance-assessment.md    # Scalability and bottlenecks
  └── modernization-roadmap.md     # Prioritized improvement plan
```

**Document Guidelines for Audit Mode:**
- Lead with metrics and numbers
- Include visualizations where possible (tables, matrices)
- Show code snippets only for critical hotspots
- Each finding should have a severity score
- Group by business impact, not technical categories

The agent will provide an objective, metrics-driven assessment with clear priorities for improvement.