---
allowed-tools: Task, Glob
argument-hint: <project idea> [optional: output-path]
description: Create a lean, engineering-focused PRD optimized for agent consumption (2-4 pages)
---

Create a lean, focused Product Requirements Document (PRD) for the provided project idea using the ken-norton-prd-expert agent. This command generates concise PRDs optimized for technical audiences and downstream agent processing.

## Usage
`/create-lean-prd "<project idea>" <output path>`

Example:
`/create-lean-prd "A mobile app for tracking personal carbon footprint" lean-prd.md`

## Process

1. **Parse Arguments**:
   - Extract the project idea from `$ARGUMENTS` (first part, may be in quotes)
   - Extract the output file path (second part, typically ending in .md)
   - If no output path is provided, default to `lean-prd.md` in the current directory

2. **Validate Inputs**:
   - Ensure the project idea is provided and meaningful
   - Check if the output path directory exists (create if needed)
   - Verify write permissions for the output location

3. **Generate Lean PRD**:
   - Use the Task tool to launch the ken-norton-prd-expert agent
   - Provide the agent with a specific prompt for lean PRD creation:
   ```
   Please create a LEAN Product Requirements Document (PRD) for the following project idea:

   [PROJECT IDEA]

   **IMPORTANT: Create a concise, engineering-focused PRD with ONLY these sections:**

   ## 1. Problem Statement & Goals
   - What specific problem are we solving? (1-2 paragraphs)
   - What are the measurable goals? (3-5 bullet points)
   - What are the explicit non-goals? (2-3 bullet points)
   - How will we measure success? (3-5 specific metrics)

   ## 2. User Context
   - Who are the primary users? (brief personas, 2-3 sentences each)
   - What are the key user stories? (5-8 most important stories)
   - What is the current vs desired experience? (brief comparison)

   ## 3. Core Requirements
   - Must Have features (5-7 items, one line each)
   - Should Have features (3-5 items, one line each)
   - Nice to Have features (2-3 items, one line each)
   - Explicitly out of scope (3-5 items to prevent scope creep)

   ## 4. Technical Context
   - High-level architecture approach (1 paragraph)
   - Key technical constraints (3-5 bullet points)
   - Major dependencies or integrations (list with brief descriptions)
   - Data requirements (what we need to store/process)

   ## 5. Risks & Assumptions
   - Critical risks (3-5 with one-line mitigation strategies)
   - Key assumptions we're making (3-5 bullet points)
   - Open questions requiring answers (3-5 items)

   **LENGTH REQUIREMENT:** Keep the entire document to 2-4 pages (approximately 500-1000 words).
   Focus on clarity and actionable information. Skip background context, market analysis,
   go-to-market strategies, and detailed timelines. This PRD is for engineering teams and
   technical planning, not business stakeholders.

   Apply Ken Norton's principles of clarity and pragmatism, but in this condensed format.

   **OUTPUT INSTRUCTIONS:**
   1. Use the Write tool to save the PRD directly to: [FULL PATH TO OUTPUT FILE]
   2. After saving, return ONLY a brief summary (3-5 bullets) of what was created
   3. DO NOT return the full document content - just confirm it was saved and provide the summary
   ```

4. **Process Agent Response**:
   - **CRITICAL: DO NOT read the saved document - the agent has already saved it correctly**
   - Receive the agent's summary of what was created
   - Do NOT use Read tool to view the document
   - Do NOT attempt to modify the file
   - Inform the user that the lean PRD has been created
   - Show the file path where it was saved
   - Display the agent's summary
   - Highlight that this is optimized for:
     - Agent consumption in pipelines
     - Quick technical understanding
     - Rapid iteration cycles
   - Suggest next steps (domain modeling, C4 architecture, etc.)