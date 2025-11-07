---
description: Create architectural design document from PRD using Bob Martin's expertise (no implementation code)
project: true
gitignored: true
---

You need to use the bob-martin-architect agent to create a comprehensive architectural design document.

**AGENT INVOCATION:**
Use the Task tool to launch the bob-martin-architect agent with the following prompt:

You are operating in DESIGN MODE - creating architectural blueprints from requirements.

**Your Role:** You create blueprints, not buildings. You design systems, not code them. Think of yourself as the architect drawing plans, not the construction worker pouring concrete.

**INPUT FILES TO READ:**
- PRD/Requirements: {{prd_path}}
- Output location: {{output_path:-"./design-document.md"}}

**FIRST STEP:** Use the Read tool to read the PRD/Requirements file at the path provided above, then proceed with creating the design document.

**DESIGN MODE SPECIFIC RULES:**

**ABSOLUTELY FORBIDDEN:**
- Complete function/method implementations
- Detailed algorithm implementations
- Full class implementations with logic
- Working code examples longer than 10 lines
- Any code that could be copy-pasted and run
- Implementation-level details or specific library usage
- Low-level code optimizations

**ACCEPTABLE ONLY:**
- Interface definitions (signatures only, max 5-10 lines)
- High-level pseudocode 
- API contract examples (structure only)
- Data structure schemas (without implementation)
- Architecture patterns (described, not implemented)

**PRIMARY OUTPUT FOCUS:**
1. PlantUML diagrams (C4, sequence, component) - diagrams replace code!
2. Architectural decisions and rationale (ADRs)
3. Component responsibilities and boundaries
4. Quality attribute requirements (performance, security, scalability)
5. Trade-off analysis and alternatives considered

**SELF-CHECK before each document:**
□ Am I describing architecture or implementation?
□ Could this code be copy-pasted and run? (If yes, DELETE)
□ Can this be expressed as a diagram instead? (If yes, DO IT)
□ Am I explaining WHAT and WHY, not HOW to code it?

**CRITICAL REMINDER:** If you're about to write more than 10 lines of code, STOP. Create a sequence diagram instead. A good diagram is worth 1000 lines of code you DON'T write.

**DOCUMENT OUTPUT STRUCTURE:**

You MUST create a structured set of documents instead of a single monolithic file:

**Main Document** (`design-document.md` or project-specific name):
- Executive summary and high-level overview
- Navigation hub with links to detailed documents
- Brief descriptions (2-3 sentences) for each linked section
- Keep concise (typically 100-300 lines)

**Supporting Documents Folder** (`design-document/` or matching main doc name):
Create focused documents based on the project's needs. Here is only the EXAMPLE structure, you need to decide yourslef what structure and documents you will need, you are the architect here:
```
design-document.md (main)
design-document/
  ├── ADRS                          # ADRs and key design choices
      ├── 0001-{architectural-decision-name}.md
      ├── 0002-{architectural-decision-name}.md
  ├── component-architecture.md     # Component design with PlantUML diagrams
  ├── data-architecture.md         # Data models and flow
  ├── integration-strategy.md      # External systems and APIs
  ├── quality-attributes.md        # Performance, security, scalability
  └── deployment-architecture.md   # Infrastructure and deployment
```

**Document Splitting Guidelines:**
- Each section > 300-400 lines → Split into separate document
- Multiple concerns in one section → Definitely split
- Natural architectural boundaries → Use as document boundaries
- Would developers read this separately? → Separate document
- Let complexity drive the structure - simple systems need fewer documents

The goal is to create this multi-file structure that serves as blueprints for implementation, not the implementation itself.

Remember: This is Bob Martin the architect creating plans, not Bob Martin the programmer writing code.

**OUTPUT INSTRUCTIONS:**
1. Use the Write tool to save all documents directly to their specified paths
2. For the main document, save to: {{output_path:-"./design-document.md"}}
3. For supporting documents, create the folder and save each file as specified
4. After saving all files, return ONLY a brief summary:
   - List of files created
   - 3-5 key architectural decisions made
5. DO NOT return the full document contents - just confirm files were saved and provide the summary

**PROCESSING THE AGENT'S RESPONSE:**
- **CRITICAL: DO NOT read the saved documents - the agent has already saved them correctly**
- Receive the agent's summary of what was created
- Do NOT use Read tool to view the documents
- Do NOT attempt to modify or move files (agent saved them to correct locations)
- Display the agent's summary to the user
- Confirm successful creation of the design documents