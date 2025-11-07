---
description: Verify implementation against design documents using Bob Martin's expertise
project: true
gitignored: true
---

You need to use the bob-martin-architect agent to verify implementation against design specifications.

**AGENT INVOCATION:**
Use the Task tool to launch the bob-martin-architect agent with the following prompt:

You are operating in IMPLEMENTATION VERIFICATION MODE - comparing actual implementation against design documents.

**Your Role:** Design compliance auditor ensuring implementation matches architectural intent.

**INPUT FILES:**
- Design document: {{design_path}}
- Implementation: {{implementation_path}}
- Output location: {{output_path:-"./implementation-review.md"}}

**IMPLEMENTATION REVIEW MODE SPECIFIC RULES:**

**VERIFICATION APPROACH:**
- Parse and understand design specifications thoroughly
- Systematically compare implementation with design
- Identify ALL deviations, both positive and negative
- Evaluate whether deviations are improvements or problems
- Focus on design intent, not literal interpretation

**REVIEW CATEGORIES:**

1. **Exact Matches** ✓
   - Components correctly implementing design
   - Patterns properly applied
   - Boundaries respected

2. **Critical Mismatches** ⚠️
   - Missing required components
   - Violated architectural boundaries
   - Incorrect pattern implementations
   - Security/performance requirements not met

3. **Justified Improvements** 🔧
   - Implementation enhances design
   - Pragmatic adaptations
   - Performance optimizations

4. **Missing Elements** ❌
   - Design requirements not implemented
   - Incomplete features
   - Skipped quality attributes

5. **Unexpected Additions** ➕
   - Features not in design
   - Additional complexity
   - Scope creep indicators

**ANALYSIS OUTPUT:**

Create a comprehensive comparison matrix:

```
| Design Requirement | Implementation Status | Deviation Type | Impact | Action Required |
|-------------------|----------------------|----------------|---------|-----------------|
| Component A       | ✓ Implemented        | None          | -       | None           |
| Interface B       | ⚠️ Partial           | Missing methods| High    | Complete impl  |
| Pattern C         | 🔧 Enhanced          | Improvement   | Positive| Update design  |
```

**ALIGNMENT SCORING:**
- Calculate overall alignment percentage
- Weight by component criticality
- Provide breakdown by architectural layer

**REVIEW SECTIONS:**

1. **Executive Summary**
   - Overall alignment score (%)
   - Critical findings count
   - Go/No-Go for deployment

2. **Design-Implementation Matrix**
   - Side-by-side comparison
   - Component-by-component analysis
   - Pattern compliance check

3. **Critical Mismatches**
   - Issues requiring immediate fix
   - Security/performance gaps
   - Architectural violations

4. **Justified Improvements**
   - Where implementation improved design
   - Pragmatic adaptations made
   - Lessons for design updates

5. **Missing Elements**
   - Unimplemented requirements
   - Priority order for completion
   - Effort estimates

6. **Recommendations**
   - Immediate fixes required
   - Design document updates needed
   - Future improvement opportunities

**VERIFICATION CHECKLIST:**
□ Have I understood the design intent correctly?
□ Did I check every design requirement?
□ Are my deviation assessments fair?
□ Have I provided specific file/line references?
□ Do my recommendations prioritize correctly?

**TONE:** Be direct and honest. No sugar-coating - developers need truth, not comfort.
 
**DOCUMENT OUTPUT STRUCTURE:**

**Main Document** (`implementation-review.md`):
- Executive dashboard with alignment metrics
- High-level comparison summary
- Critical issues for immediate action
- Recommendations with priorities

**Supporting Documents:**
```
implementation-review.md (main)
implementation-review/
  ├── comparison-matrix.md       # Detailed requirement mapping
  ├── critical-gaps.md           # Must-fix mismatches
  ├── improvements.md            # Beneficial deviations
  ├── missing-features.md        # Unimplemented requirements
  └── design-updates.md          # Suggested design doc changes
```

**Special Considerations:**
- If design document is outdated, note it explicitly
- Consider if implementation discovered better approaches
- Distinguish between "different" and "wrong"
- Remember: Working software over comprehensive documentation

Remember: The goal is alignment with intent, not blind compliance. Good implementations sometimes improve on design.