Read [project-path] and analyze the implementation of [feature], including all related:
- controllers
- services
- models
- routes
- UI components

Then, reconstruct this feature as a standalone service documentation under:
@okta-tech-docs/docs/services/[feature-name]

The documentation should follow the same structure and conventions as existing services, and include:

- overview.md
- user-experience/*.md (flows, user journeys, edge cases)
- pages/*.md (UI structure and behavior)
- tech/
  - architecture.md
  - models/*.md
  - data_handling/*.md
  - service_functions/*.md
  - permissions.md
  - tenancy.md (if applicable)

External Constraints & Adaptation Guidelines:
These are limitations from the target system context and rules for adapting the feature into the new architecture.
- 
- 
- 

External Dependencies & Reference Files:
- 
- 
- 

Requirements:
- Do not copy code directly; abstract the logic into a clean service design
- Do not reference or expose dependency sources as implementation references within other documentation files. They must only be listed as conceptual dependencies, not explained or expanded as part of feature documentation.
- All external constraints and adaptation guidelines must be abstracted into architectural principles. Do not copy or closely mirror the original wording; instead, express the intent in a generalized system design form.
- Treat the source project strictly as an implementation reference. Do not describe or document it as a system. All output must be framed from the perspective of the target architecture only.
- Provide both high-level and low-level documentation
- Use consistent naming conventions
- Include examples (API, data, flows)
- Write in clean, structured Markdown
- Document by [Language] Language.