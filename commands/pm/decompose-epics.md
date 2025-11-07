---
description: "Decompose design document into user story epics using Jeff Patton's story mapping approach"
argument-hint: "<design-doc-path> [optional: output-path]"
allowed-tools: "Read, Glob, Task, Write"
---

# Decompose Design Document to Epics

Parse the arguments to extract the design document path and optional output path from: `$ARGUMENTS`

Read the design document and any related files that might provide context about the project.

Then launch the Jeff Patton PM agent to decompose the design into epics:

```
Use the Task tool to launch the jeff-patton-pm agent with the following prompt:

"I need you to decompose this design document into user story epics using your story mapping methodology.

Design Document:[Path to the design document]

Please:
1. Extract the user journey and identify the backbone (main user activities)
2. Group functionality into epics that deliver vertical slices of value
3. Sequence epics into releases (MVP/walking skeleton first)
4. Ensure each epic delivers end-to-end user value and can be completed in 1-2 sprints

Create a structured epic decomposition document with:
- User Journey Backbone
- Release Plan with walking skeleton first
- Detailed epics with user stories, acceptance criteria, and sizing
- Dependencies and risks
- Story mapping visualization

Focus on ensuring every epic closes a user loop and delivers real value. Challenge any technical layers and push for the thinnest possible slices that still work end-to-end."
```

After receiving the agent's response, save the epic decomposition to the specified output path or to `docs/epic-decomposition.md` if no path was provided.