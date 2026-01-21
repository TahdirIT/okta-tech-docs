## Security (Proposal/Auto Generated)

### Old Project (Tahdir)
- Authentication: Basic authentication mechanisms
- Authorization: Role-based access control (RBAC)
- Data Exposure: Sequential IDs exposed in URLs and APIs
- Encryption: Basic HTTPS/TLS
- Secrets Management: Environment variables managed via GitHub Actions secrets
- API Security: Basic API authentication
- Input Validation: Framework-level validation
- Security Headers: Basic security headers
- Vulnerability Scanning: Manual security reviews

### New Project (Okta v1 - In-scope decisions) 
- Authentication: Enhanced authentication with multi-factor authentication (MFA)
- Authorization: Role-based access control (RBAC) with fine-grained permissions
- Data Exposure: Using ULID as exposed ID in each model among services and publicity
- Encryption: End-to-end encryption for sensitive data, HTTPS/TLS
- Secrets Management: Secure secrets management with encrypted storage
- API Security: API authentication with JWT tokens, rate limiting
- Input Validation: Comprehensive input validation and sanitization
- Security Headers: Enhanced security headers (CSP, HSTS, X-Frame-Options)
- Vulnerability Scanning: Automated security scanning in CI/CD pipeline
- Security Monitoring: Security event logging and monitoring

### Feature Project (Okta - Out of Scope)
- Authentication: OAuth 2.0 / OpenID Connect (OIDC) with SSO
- Authorization: Attribute-based access control (ABAC) with policy engines
- Data Exposure: ULID with additional security layers for sensitive data
- Encryption: Field-level encryption, database encryption at rest
- Secrets Management: Secrets management with Vault / AWS Secrets Manager
- API Security: API Gateway with OAuth 2.0, API keys, mTLS
- Input Validation: Advanced validation with schema validation and WAF
- Security Headers: Comprehensive security headers with CSP policies
- Vulnerability Scanning: Continuous security scanning with SAST/DAST tools
- Security Monitoring: SIEM integration with real-time threat detection
- Zero-Trust Security: Zero-trust network architecture with service mesh
- Security Auditing: Comprehensive audit logging and compliance reporting
- Penetration Testing: Regular automated and manual penetration testing
- Security Compliance: SOC 2, ISO 27001 compliance frameworks
