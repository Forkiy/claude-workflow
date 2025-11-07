---
description: "Facilitate an interactive story mapping workshop with Jeff Patton's methodology"
argument-hint: "[optional: project-description-or-doc-path]"
allowed-tools: "Read, Task"
---

# Story Mapping Workshop Facilitation

If a project document path is provided in `$ARGUMENTS`, read it first to understand the context.

Then launch the Jeff Patton PM agent to facilitate the workshop:

```
Use the Task tool to launch the jeff-patton-pm agent with the following prompt:

"I need you to facilitate an interactive story mapping workshop to help define our epic structure.

[If project context was provided, include:]
Project Context:
[Include the content of any provided documentation]

Please run this as an interactive workshop where you:
1. Guide discovery of the user journey backbone through questions
2. Help identify user activities and tasks collaboratively
3. Facilitate finding the walking skeleton (thinnest MVP)
4. Guide the team to package tasks into properly-sized epics
5. Challenge any technical thinking and push for user outcomes

Start with understanding who the users are and what they're trying to accomplish. Then progressively build the story map through discussion, not prescription.

Use your facilitative, coaching style to help the team discover the best decomposition themselves. Ask probing questions, challenge horizontal thinking, and keep focus on user value.

The workshop should be interactive - ask questions, wait for responses, and build the map together rather than creating it all at once."
```

Facilitate the interactive workshop with the user, building the story map progressively through their responses.