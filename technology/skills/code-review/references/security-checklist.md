# Security Checklist for Code Review

Quick reference for the OWASP Top 10 and common security issues to check during code review.

## OWASP Top 10 Quick Reference

| # | Risk | What to Look For | Red Flag Code Pattern |
|---|------|-----------------|----------------------|
| A01 | Broken Access Control | Missing auth checks on routes/endpoints | No `authorize()` / `isAuthenticated()` check before data access |
| A02 | Cryptographic Failures | Hardcoded secrets, weak hashing, unencrypted PII | `password = "secret"`, `MD5(password)`, PII in plain text DB column |
| A03 | Injection | SQL/NoSQL/OS/LDAP injection via unsanitized input | `query = "SELECT * FROM users WHERE id = " + userId` |
| A04 | Insecure Design | Missing threat modeling, no rate limiting | No rate limit on login endpoint, no account lockout |
| A05 | Security Misconfiguration | Debug mode in prod, default credentials, verbose errors | `DEBUG=True`, stack traces returned to user |
| A06 | Vulnerable Components | Outdated dependencies with known CVEs | Check `npm audit`, `pip-audit`, `trivy` output |
| A07 | Auth Failures | Weak session management, no MFA, predictable tokens | Short-lived tokens not invalidated on logout |
| A08 | Data Integrity Failures | Unverified deserialization, unsigned updates | `pickle.loads(user_input)`, no signature on update payload |
| A09 | Logging Failures | No audit trail, passwords in logs | `logger.info(f"Login attempt: {username} / {password}")` |
| A10 | SSRF | User-controlled URLs fetched by server | `requests.get(user_supplied_url)` with no allowlist |

## High-Frequency Issues by Language

### JavaScript / TypeScript
- `eval()` or `new Function()` with user input → code injection
- `innerHTML = userInput` → XSS
- `require(userInput)` → arbitrary module loading
- Unvalidated `JSON.parse()` input
- `child_process.exec(userInput)` → shell injection

### Python
- `os.system(userInput)` or `subprocess.shell=True` with user input
- `pickle.loads()` on untrusted data
- `exec()` / `eval()` with user input
- SQLAlchemy raw queries: `session.execute(f"SELECT ... {user_input}")`

### SQL
- String concatenation in queries → use parameterized queries always
- Missing `WHERE` clause on UPDATE/DELETE
- Overly permissive DB user (should not have DROP or admin rights in app)

## Secrets & Credentials Checklist

- [ ] No API keys, tokens, or passwords in source code
- [ ] `.env` files are in `.gitignore`
- [ ] Secrets loaded from environment variables or a secrets manager (Vault, AWS Secrets Manager)
- [ ] No secrets in logs, error messages, or API responses
- [ ] Tokens scoped to minimum required permissions

## Data Handling Checklist

- [ ] PII (names, emails, phone numbers) encrypted at rest
- [ ] PII not logged in plaintext
- [ ] Credit card / payment data not stored (use a payment processor)
- [ ] Data retention policy enforced (delete after X days)
- [ ] User data not exposed across account boundaries
