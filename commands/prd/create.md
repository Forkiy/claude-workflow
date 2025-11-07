---
allowed-tools: Task, Write, Read, Glob, Fetch
argument-hint: <project idea> [optional: output-path]
description: Create a Product Requirements Document (PRD) using Ken Norton's methodology
---

Create a comprehensive Product Requirements Document (PRD) for the provided project idea using the ken-norton-prd-expert agent.

**Note:** This command creates a COMPREHENSIVE business PRD with 10 sections including go-to-market strategy, sales enablement, and detailed appendices. For a lean, engineering-focused PRD (2-4 pages) optimized for agent pipelines, use `/create-lean-prd` instead.

## Usage
`/create-prd "<project idea>" <output path>`

Example:
`/create-prd "A mobile app for tracking personal carbon footprint" carbon-tracker-prd.md`

## When to Use This Command
- Creating PRDs for business stakeholders
- Need comprehensive market analysis and GTM strategy
- Formal documentation for enterprise projects
- When multiple teams need alignment (engineering, design, sales, marketing)

## Process

1. **Parse Arguments**:
   - Extract the project idea from `$ARGUMENTS` (first part, may be in quotes)
   - Extract the output file path (second part, typically ending in .md)
   - If no output path is provided, default to `prd.md` in the current directory

2. **Validate Inputs**:
   - Ensure the project idea is provided and meaningful
   - Check if the output path directory exists (create if needed)
   - Verify write permissions for the output location

3. **Generate PRD**:
   - Use the Task tool to launch the ken-norton-prd-expert agent
   - Provide the agent with a detailed prompt including:
     - The project idea/description
     - Request for a comprehensive PRD following Ken Norton's methodology
     - Instructions to create a complete, production-ready document
   - The prompt should be something like:
     ```
     Please create a comprehensive Product Requirements Document (PRD) for the following project idea:

     [PROJECT IDEA]

     Create a COMPREHENSIVE business-ready PRD with the following sections:

     ## 1. Overview
     - Problem statement (what problem are we solving?)
     - Goals (what are we trying to achieve?)
     - Non-Goals (what are we explicitly NOT doing?)
     - Success Metrics (how will we measure success? - quantifiable)

     ## 2. Background & Strategic Fit
     - Why Now? (market timing and opportunity)
     - Strategic Context (how this fits company/product strategy)
     - Supporting Data (research, user feedback, competitive intel)

     ## 3. User Stories & Use Cases
     - Target Users (who are we building for?)
     - User Scenarios (what are they trying to accomplish?)
     - Current Experience (what's broken today?)
     - Desired Experience (what should the ideal experience be?)

     ## 4. Requirements
     - Functional Requirements (prioritized as Must Have, Should Have, Nice to Have)
     - Non-Functional Requirements (performance, security, accessibility, scalability)
     - Explicitly Out of Scope (what we're NOT building - prevents scope creep)

     ## 5. User Experience
     - Key User Flows (step-by-step experiences)
     - Wireframes/Mockups (visual representation when applicable)
     - Design Principles (UX guidelines for this feature)

     ## 6. Technical Considerations
     - Architecture Overview (high-level technical approach)
     - Dependencies (what systems/services does this rely on?)
     - Data Requirements (what data do we need to collect/store/process?)
     - Integration Points (APIs, third-party services)

     ## 7. Go-to-Market
     - Launch Strategy (phased rollout, beta, full launch?)
     - Positioning & Messaging (how do we talk about this?)
     - Sales/Support Enablement (what do teams need to know?)
     - Marketing Plan (how do we announce/promote?)

     ## 8. Timeline & Resources
     - Key Milestones (major deliverables and dates)
     - Team Requirements (who do we need? - eng, design, QA, etc.)
     - Dependencies & Blockers (what needs to happen first?)

     ## 9. Risks & Open Questions
     - Technical Risks (what could go wrong technically?)
     - Business Risks (market, competitive, or resource risks)
     - Open Questions (what don't we know yet? who needs to answer?)
     - Mitigation Strategies (how do we address known risks?)

     ## 10. Appendix
     - User Research (links to studies, interviews, surveys)
     - Competitive Analysis (what are competitors doing?)
     - Data & Analytics (supporting metrics and trends)
     - Glossary (domain-specific terms)
     - References (related documents, RFCs, design docs)

     Follow Ken Norton's PRD best practices for clarity and comprehensiveness.
     This is a complete business document for all stakeholders (engineering, design, business, GTM).

     Save the PRD to @[PATH TO SAVE THE PRD]
     ```

4. **Provide Summary**:
   - Take the output from the ken-norton-prd-expert agent
   - Inform the user that the PRD has been created
   - Show the file path where it was saved
   - Provide a brief summary of the key sections included
   - Suggest next steps (review, share with team, etc.)
