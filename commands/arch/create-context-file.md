---
allowed-tools: Task, Write, Read, Glob
argument-hint: [optional: resulting-file-name]
description: Create a comprehensive context file that serves as a detailed technical reference for developers
---

Please analyze this codebase and create a comprehensive {resulting-file-name (default: CONTEXT.MD)} file that serves as a detailed technical reference for developers. Examine the actual code structure, patterns, and technologies used, then document:

  1. **System Overview Section**
     - Project type and primary purpose
     - Technology stack (frameworks, languages, runtime versions, key libraries)
     - Architectural patterns identified in the codebase
     - Data storage technology and strategy
     - Authentication/authorization approach (if present)
     - External service integrations
     - Deployment/containerization approach
     - Monitoring and logging tools

  2. **Business/Domain Context**
     - Core concepts and terminology specific to this domain
     - Key workflows and processes
     - Critical business rules and constraints
     - Domain-specific validations and logic

  3. **Directory Structure & Modification Triggers**
     For each major directory/module, document:
     - Purpose and responsibility
     - Key files and their specific roles
     - When developers should modify files in this location
     - Example trigger: "Modify when: Adding new API routes, changing request validation, updating middleware"

  4. **File Modification Matrix**
     Create a table showing what files/locations to modify for common change scenarios relevant to this project:
     - Adding new business entities/models
     - Implementing new features
     - Adding new API endpoints/routes/interfaces
     - Changing data access logic
     - Integrating external services
     - Updating database schemas/migrations
     - Modifying authentication/authorization

  5. **Code Patterns & Templates**
     Identify the actual patterns used in the codebase and provide copy-paste ready templates for:
     - Creating new entities/models (with the project's conventions)
     - Data access patterns (repositories, queries, ORMs, etc.)
     - Business logic implementation (services, handlers, use cases, etc.)
     - API/interface patterns (controllers, routes, handlers, etc.)
     - Database/persistence configuration
     - Event/messaging patterns (if present)
     - External service integration
     - Testing patterns

  6. **Configuration & Environment Management**
     - List all configuration files and their purposes
     - Environment-specific settings and override mechanisms
     - Service configuration structure with examples
     - Secrets/credentials management approach

  7. **Dependency Management & Injection**
     - How dependencies are registered/injected
     - Service lifetime patterns (if applicable)
     - Third-party client registration patterns
     - Common registration/setup helpers

  8. **Testing Strategy & Patterns**
     - Test organization and directory structure
     - Test naming conventions used in the project
     - Test setup/teardown approaches
     - Examples of different test types (unit, integration, e2e)

  9. **Performance & Scalability Considerations**
     - Caching strategies implemented
     - Database/query optimization techniques
     - Resilience patterns (retries, circuit breakers, timeouts)
     - Async/concurrent processing approaches

  10. **Build, Deployment & Infrastructure**
      - Build configuration and process
      - Containerization setup (Docker, etc.)
      - CI/CD integration points
      - Health check/monitoring setup
      - Environment-specific deployment steps

  11. **Security Practices**
      - Authentication and authorization mechanisms
      - API security measures
      - Input validation and sanitization
      - Secure configuration practices

  12. **External Dependencies & Integrations**
      - Package/library dependencies with versions
      - External APIs/services with authentication methods
      - Integration patterns and data flows

  13. **Error Handling & Observability**
      - Logging patterns and levels
      - Error handling strategies
      - Monitoring/telemetry integration
      - Debugging approaches

  **Instructions:**
  - Analyze the actual codebase structure to determine what sections are relevant
  - Include specific file paths, class/function names, and real code snippets from the project
  - Provide actionable, copy-paste ready templates following the project's existing conventions
  - Use clear markdown formatting with code blocks, tables, and examples
  - Focus on practical guidance: "Where do I add X?", "What pattern for Y?", "What files for Z?"
  - If certain sections don't apply (e.g., no external services), omit or note as "Not applicable"
  - Adapt the depth and technical language to match the project's complexity and stack

  **Output format:**
  - It should be a single file in Markdown format
  - Do not insert big code blocks; use code to illustrate common patterns and naming conventions