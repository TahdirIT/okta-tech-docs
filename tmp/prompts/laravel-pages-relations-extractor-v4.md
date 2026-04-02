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
    relation: <navigation|parent-child|form|auth>
  - to: <target-page>
    relation: <navigation|parent-child|form|auth>

# =========================
# PAGE NAME RULE
# =========================

Page name must be derived from:
- route name (preferred)
- OR URI path
- OR controller action

Normalize to kebab-case.

Example:
UserLoginController → user-login
/dashboard → dashboard-home

# =========================
# IMPORTANT RULES
# =========================

1. DO NOT output JSON.
2. DO NOT output a combined global list.
3. Each file MUST contain only relations starting from ONE "from" page.
4. Ignore API-only endpoints unless they return UI views.
5. Infer missing relations when obvious (e.g. login → dashboard).
6. Include authentication-related relations (login/register/logout flows).
7. Respect multi-tenant or subdomain context if present.
8. DO NOT include technical execution details such as internal routing mechanics.

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
- The component is the only way to reach a critical flow step (e.g. auth completion), OR
- The user explicitly asks to include global nav relations.

4) If a relation appears only because of a reused component across sibling pages, drop it to avoid mesh-like duplication.

# =========================
# ANALYSIS STRATEGY (CRITICAL)
# =========================

You MUST NOT scan and process the entire project at once.

Follow incremental analysis:

STEP 1:
- Scan ONLY route definitions (web routes files)
- Identify a small batch of pages (5-10 max)

STEP 2:
- Analyze ONLY related files:
  controllers, blade templates, Livewire files, and route definitions

STEP 3:
- Extract relations ONLY for that batch

STEP 4:
- Generate YAML files for those "from" pages immediately

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
    relation: auth
