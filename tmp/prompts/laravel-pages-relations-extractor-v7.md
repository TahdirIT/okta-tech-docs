You are an expert Laravel system analyzer.

Your task is to extract all user navigation relations in the Laravel project located at:
{{path-to-project-to-be-analyzed}}

and generate structured YAML files.

# =========================
# OUTPUT STRUCTURE
# =========================

All output files must be generated inside this directory:

{{generated/page-relations/}}

Each file represents ONE source page (FROM page).

File naming rule:
<from-page>.yaml

Example:
generated/page-relations/landing-page.yaml
generated/page-relations/user-login.yaml

# =========================
# FILE FORMAT (YAML)
# =========================

Each file must follow this structure:

from: <page-name>
relations:
  - to: <target-page>
    relation: <navigation|parent-child|form>
  - to: <target-page>
    relation: <navigation|parent-child|form>

# =========================
# PAGE NAME RULE
# =========================

Page name must be derived from:
- route name (preferred)
- OR URI path
- OR controller action

Normalize to kebab-case.

Example:
UserLoginController -> user-login
/dashboard -> dashboard-home

# =========================
# IMPORTANT RULES
# =========================

1. DO NOT output JSON.
2. DO NOT output a combined global list.
3. Each file MUST contain only relations starting from ONE "from" page.
4. Ignore API-only endpoints unless they return UI views.
5. Infer missing relations when obvious (e.g. login -> dashboard).
6. Respect multi-tenant or subdomain context if present.
7. DO NOT include technical execution details such as internal routing mechanics.

# =========================
# COMPONENT & UI LOGIC RULE (CRITICAL)
# =========================

- DO NOT treat shared UI components (e.g. tab headers, layouts, sidebars, navbars) as navigation sources by default.
- ONLY include a component if it results in an actual route/page transition.
- If multiple pages share the same component (e.g. tabs layout), do NOT create mesh-like relations between them unless:
  - clicking the tab triggers a real route change, OR
  - it clearly maps to a distinct URL/view transition.
- Ignore purely visual or structural reuse of components.
- Never infer navigation relations from shared Blade/Livewire components alone.

# =========================
# SHARED COMPONENT FILTER (STRICT)
# =========================

When extracting relations from a page:

1) Classify each link source as one of:
- page-local content (inside the page's own main content/body)
- shared navigation component (sidebar, tabs, navbar, layout, header/footer partials, reused includes/components)

2) EXCLUDE links from shared navigation components by default, even if they are clickable route transitions.

3) INCLUDE shared-component links only if at least one is true:
- The component is unique to this page (not reused by sibling pages), OR
- The component is the only way to reach a critical flow step, OR
- The user explicitly asks to include global nav relations.

4) If a relation appears only because of a reused component across sibling pages, drop it to avoid mesh-like duplication.

# =========================
# MODULE HIERARCHY FALLBACK (ANTI-EMPTY RULE)
# =========================

If strict shared-component filtering removes most or all intra-module relations, infer safe hierarchy relations from route naming/prefixes to avoid empty or misleading graphs.

Definitions:
- Module hub page: parent route/page that lists or owns a feature module (example: settings-countries)
- Child page: route/page under the module namespace (example: settings-country-stages)

Rules:
1) Infer parent-child structure from route names and URI prefixes, not from shared nav components.
2) Add hub -> child relations using:
   relation: parent-child
3) Add child -> hub relations using:
   relation: parent-child
4) Do NOT add child -> child relations unless there is explicit page-local evidence (link/form/action) in the child page itself.
5) Keep hierarchy strictly structural based on routes/modules only.

# =========================
# RELATION TYPE DECISION ORDER
# =========================

For each discovered transition, choose relation type in this priority order:
1) form
2) parent-child
3) navigation

If multiple types match, keep the highest-priority type only.

# =========================
# FILE GENERATION RULE (CRITICAL)
# =========================

- ONLY generate a `<from-page>.yaml` file IF AND ONLY IF it contains at least one valid `to` relation.
- If a page has no outgoing relations after filtering and inference, DO NOT create any YAML file for it.
- This rule applies strictly, even if the page exists or is reachable in the route list.

# =========================
# ANALYSIS STRATEGY (CRITICAL)
# =========================

You MUST NOT scan and process the entire project at once.

Follow incremental analysis:

STEP 1:
- Scan ONLY route definitions (web routes files)
- Identify a small batch of pages (5–10 max)

STEP 2:
- Analyze ONLY related files:
  controllers, blade templates, Livewire files, and route definitions

STEP 3:
- Extract relations ONLY for that batch

STEP 4:
- Generate YAML files for those "from" pages immediately (only if they have relations)

STEP 5:
- Continue iteratively until project is fully covered

# =========================
# CONTEXT CONTROL RULE
# =========================

Never attempt full project analysis in one pass.

Always:
- work in small batches
- analyze incrementally
- write outputs immediately
- only emit files when valid
- then continue

# =========================
# OUTPUT EXAMPLE
# =========================

File: generated/page-relations/landing-page.yaml

from: landing-page
relations:
  - to: user-login
    relation: navigation

  - to: register-tenant
    relation: navigation

  - to: dashboard-home
    relation: navigation