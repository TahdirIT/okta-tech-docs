Read {{project-path}} and analyze the implementation of {{feature}}, including all related:
- controllers
- services
- models
- routes
- UI components

Then, reconstruct this feature as a standalone service documentation under:
@okta-tech-docs/docs/services/{{feature-name}}

The documentation should follow the same structure and conventions as existing services, and include:

- overview.md
- user-journeys/<role>.md
- user-flows/<role>.<user-flow>.md

---

User Journey File Content Requirements:
Each user-journey/<role>.<service>.md file must describe the end-to-end experience of a single role using the service from a user perspective (NOT implementation).

Each file must include the following sections:

- Role Overview (who the user is and what they aim to achieve)
- Goals / Intentions (main objectives of the role within the service)
- Entry Points (how the user accesses the service)
- End-to-End Journey (step-by-step user flow from entry to completion of task)
- Key Actions Available to the Role (create, update, delete, view, approve, publish, etc.)
- System Feedback & States (loading, success, errors, empty states, permission denied)
- Business Rules (user-facing rules only, not technical logic)
- Role Limitations / Permissions (what the role cannot do or access)
- Alternate Paths / Edge Cases (failures, missing data, denied actions)

Constraints for User Journey files:
- Must be written from a pure user experience perspective
- Must NOT include implementation details (no controllers, services, models, routes, or APIs)
- Must NOT describe backend architecture or system internals
- Must focus only on user-visible behavior and outcomes
- Must describe flows as sequential user steps, not system logic

---

External Constraints & Adaptation Guidelines:
These are limitations from the target system context and rules for adapting the feature into the new architecture.
-
-
-

External Dependencies & Reference Files:
-
-
-

---

Requirements:
- Do not copy code directly; abstract the logic into a clean service design
- Do not reference or expose dependency sources as implementation references within other documentation files. They must only be listed as conceptual dependencies, not explained or expanded as part of feature documentation.
- All external constraints and adaptation guidelines must be abstracted into architectural principles. Do not copy or closely mirror the original wording; instead, express the intent in a generalized system design form.
- Treat the source project strictly as an implementation reference. Do not describe or document it as a system. All output must be framed from the perspective of the target architecture only.
- Provide both high-level and low-level documentation
- Use consistent naming conventions
- Write in clean, structured Markdown
- Document by {{Language}} Language