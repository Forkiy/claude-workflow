---
description: "Validate epic decomposition using Jeff Patton's story mapping principles"
argument-hint: "<epic-doc-path>"
allowed-tools: "Read, Task"
---

# Validate Epic Decomposition

Parse the epic document path from: `$ARGUMENTS`

Then launch the Jeff Patton PM agent to validate the epics:

```
Use the Task tool to launch the jeff-patton-pm agent with the following prompt:

"I need you to review and validate this epic decomposition against story mapping best practices.

Epic Decomposition Document:
[Path to the epic document]

Please validate:
1. Each epic delivers a vertical slice (end-to-end user value)
2. Epics are appropriately sized (1-2 sprints ideal)
3. The release sequence follows user journey and tests assumptions early
4. The MVP/walking skeleton closes at least one user loop
5. No horizontal layers masquerading as epics

Provide a validation report that includes:
- Overall assessment (STRONG / NEEDS WORK / REQUIRES MAJOR REVISION)
- Epic-by-epic analysis with specific issues
- Anti-patterns detected (horizontal slicing, feature factory thinking, technical epics)
- Specific recommendations for improvement
- Questions for the team to discuss

For each issue found, explain WHY it matters for user value delivery and provide a specific alternative."
```

Display the validation report to the user.