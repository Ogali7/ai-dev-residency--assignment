---
name: security-code-review
description: Reviews application code for security problems, with extra care for apps that handle money, personal, or financial data. Covers secrets and API keys, input handling, login and sessions, who can access what, data protection, and dependencies. Use this whenever someone asks for a security review, a security check, or asks if their code, API, database, or login is safe. Also use it before code is pushed or deployed, and after adding login, payments, forms, file uploads, or anything that stores user data, even if the user did not mention security.
---

# Security Code Review

Review the provided code and decide whether it is safe to ship. Work through all six checks below in order. Do not skip a check, even if the code looks fine at a glance. Read the actual code and config files; do not guess about files you have not opened.

## Review process

### 1. Secrets and API keys
- No passwords, API keys, tokens, or database URLs are written directly in the code.
- Secrets are loaded from environment variables, and `.env` files are listed in `.gitignore`.
- No secrets are sent to the browser. Flag keys used in front-end code or in variables exposed to the client (for example `NEXT_PUBLIC_` or `VITE_` prefixes).
- If a secret was ever committed, say it must be revoked and replaced, not just deleted, because it stays in the Git history.

### 2. Input handling
- All input from users, URLs, and other systems is checked on the server, not only in the browser.
- Database queries use parameters or an ORM. Flag queries built by joining strings with user input.
- User content shown on the page is escaped. Flag `innerHTML`, `dangerouslySetInnerHTML`, `eval`, and similar without sanitizing.
- File uploads check type and size and are not stored where they can be run as code.
- Requests to URLs supplied by users are restricted to allowed destinations.

### 3. Login and sessions
- Passwords are hashed with a slow, salted algorithm (bcrypt, scrypt, or Argon2). Flag plain text, MD5, or SHA-1.
- Login has rate limiting or lockout to slow down password guessing.
- Session cookies use `HttpOnly`, `Secure`, and `SameSite`.
- Sessions and tokens expire, and logging out ends the session on the server.
- Prefer a well-known auth library or provider over hand-written login code.

### 4. Access control
- Every request that reads or changes data checks that the logged-in user is allowed to do it, on the server.
- Users cannot see or edit another user's data by changing an ID in the URL or request.
- Admin features are protected on the server, not only hidden in the interface.
- Database rules (for example row-level security) are turned on where the platform supports it.

### 5. Data protection
- All traffic uses HTTPS.
- Only the data the app truly needs is collected and stored.
- Sensitive data (bank details, account numbers, income, health information) is encrypted at rest where possible and never written to logs.
- Error messages shown to users do not reveal stack traces, database details, or whether an email address has an account.
- Users can delete their account and data.

### 6. Dependencies and configuration
- Packages are reasonably up to date. Suggest running `npm audit` (or the equivalent for the language) and report known vulnerable packages.
- Debug mode and verbose errors are off in production.
- CORS allows only the app's own domains. Flag `*` on endpoints that use cookies or return private data.
- Security headers are set (Content-Security-Policy, Strict-Transport-Security, X-Content-Type-Options).

## Output format

Group findings under exactly these six headings, in this order:

```
## Secrets and API keys
## Input handling
## Login and sessions
## Access control
## Data protection
## Dependencies and configuration
```

- Under each heading, list issues as bullets. Each bullet names the file and line, the problem, why it is risky in one plain sentence, and a suggested code fix.
- Rate each issue **Critical**, **High**, **Medium**, or **Low**. Anything that exposes secrets, user data, or money is Critical.
- If a category has no problems, write **No issues found** under its heading. Never omit a heading.
- End with a one-line verdict: **Safe to ship** or **Not safe to ship**, with the number of Critical and High issues.
- Note that a code review does not replace security testing, and suggest a professional review before launching any app that handles real money or financial data.
