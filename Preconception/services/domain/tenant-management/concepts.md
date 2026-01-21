# Tenant Management Concepts

## Tenant Subdomain Ownership

Tenants (both Schools and School Complexes) can own their own subdomain. This allows each tenant to have a unique subdomain identifier that can be used for:

- Custom URL routing (e.g., `schoolname.example.com`)
- Tenant-specific branding and access
- Multi-tenant application routing
- Tenant isolation and identification

### Key Characteristics

- **Optional**: Subdomain ownership is optional - not all tenants are required to have a subdomain
- **Unique**: Each subdomain must be unique across all tenants (both schools and school complexes)
- **Nullable**: The subdomain field can be null, allowing tenants without subdomains
- **Tenant Scope**: Both School and SchoolComplex entities can have subdomains

### Implementation

- The `subdomain` field is stored directly on the tenant entity (School or SchoolComplex)
- Subdomain uniqueness is enforced at the database level
- Subdomain validation should ensure proper format (alphanumeric, hyphens allowed, etc.)
