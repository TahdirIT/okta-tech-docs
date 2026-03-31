You are an expert Laravel system analyzer.

Your task is to extract all user navigation flows in the Laravel project located at:
[path-to-project-to-be-analyzed]

and generate structured YAML files.

# =========================
# OUTPUT STRUCTURE
# =========================

All output files must be generated inside this directory:

generated/page-flows/

Each file represents ONE source page (FROM page).

File naming rule:
<from-page>.yaml

Example:
generated/page-flows/landing-page.yaml
generated/page-flows/user-login.yaml

# =========================
# FILE FORMAT (YAML)
# =========================

Each file must follow this structure:

from: <page-name>
flows:
  - to: <target-page>
    type: <link|redirect|form|auth-redirect>
    method: <GET|POST|PUT|DELETE|N/A>
    middleware: [<list-of-middlewares>]
    source: <blade|controller|livewire|inertia|route|inferred>

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
2. DO NOT output combined global flow list.
3. Each file MUST contain only flows starting from ONE "from" page.
4. Ignore API-only endpoints unless they return UI views.
5. Infer missing flows when obvious (e.g. login → dashboard).
6. Include authentication flows (login/register/logout/redirects).
7. Respect multi-tenant or subdomain context if present.

# =========================
# ANALYSIS STRATEGY (CRITICAL)
# =========================

You MUST NOT scan and process the entire project at once.

Follow incremental analysis:

STEP 1:
- Scan ONLY routes (web.php and route files)
- Identify a small batch of pages (5–10 max)

STEP 2:
- Analyze ONLY related files:
  controllers + blade views + livewire components

STEP 3:
- Extract flows ONLY for that batch

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

File: generated/page-flows/landing-page.yaml

from: landing-page
flows:
  - to: user-login
    type: link
    method: GET
    middleware: [guest]
    source: blade

  - to: register-tenant
    type: link
    method: GET
    middleware: [guest]
    source: blade