## GitHub security & secret-handling instructions

Your priority is to prevent **secrets and sensitive data** from being exposed in:
- the repository (commits, tags, releases)
- issues, PR descriptions, comments, discussions, wikis
- CI logs (GitHub Actions)
- artifacts (build outputs, debug bundles)

Assume any leaked credential is **compromised** and must be rotated.

### Non-negotiable rules
- **Never** hardcode secrets in code or docs (API keys, tokens, passwords, private keys, JWTs, connection strings).
- **Never** paste or echo secrets into logs (even if you *think* they will be masked).
- **Never** commit real `.env` files. Use `.env.example` (placeholders only) and `.gitignore`.
- If you suspect a secret was exposed: **stop**, recommend **rotation/revocation first**, then cleanup.

### .env files (local development)
- Use `.env` only for **local** development.
- Ensure `.env` is in `.gitignore` (and consider also ignoring variants: `.env.*`, `*.env`, `.envrc`, `*.pem`, `*.key`).
- Provide an `.env.example` (or `.env.sample`) containing:
  - only variable names and safe placeholders (e.g., `API_KEY=YOUR_API_KEY_HERE`)
  - brief comments describing where to obtain the value
  - no real hostnames/usernames if those are sensitive for your org
- Prefer environment variables over config files for secrets; load `.env` only in dev.

### GitHub Actions secrets & CI safety
- Prefer GitHub Actions **Secrets** (repo/org/environment) for CI credentials.
- Use environment-level secrets for staged deployments and add protection (required reviewers) when appropriate.
- Prefer the built-in `GITHUB_TOKEN` when it is sufficient; otherwise prefer a GitHub App token over a long-lived PAT.
- Apply **least privilege**:
  - explicitly set `permissions:` in workflows (default to read-only, elevate per job)
  - don't grant `contents: write` / `pull-requests: write` / `id-token: write` unless needed
- Don't pass secrets on command lines if avoidable (process lists / audit events may capture them). Prefer env vars or stdin.
- Mask values that are not GitHub secrets using `::add-mask::VALUE` **before** any potential output.
- Treat forked PRs and untrusted inputs as hostile:
  - secrets generally aren't available to fork-triggered workflows (plan accordingly)
  - avoid script-injection patterns; route untrusted values through intermediate env vars
- Pin third-party actions to immutable versions (ideally full commit SHA) and keep them updated.

### API tokens, API keys, and credentials
- Use **short-lived** credentials where possible (for cloud deployments, prefer GitHub Actions OIDC with temporary credentials).
- Scope credentials narrowly (single repo / minimal permissions / shortest expiration).
- Rotate credentials regularly and immediately on suspected exposure.
- Never store tokens in:
  - source files
  - committed config files
  - test fixtures
  - screenshots
  - example curl commands with real headers

### Safe examples (when writing docs or code)
- Use placeholders like:
  - `YOUR_API_KEY` / `YOUR_TOKEN`
  - `example.invalid` domains
  - `00000000-0000-0000-0000-000000000000` IDs
- When showing HTTP examples, redact:
  - `Authorization: Bearer ***`
  - cookies/session IDs
  - signed URLs

### GitHub security features to lean on
- Enable and use:
  - Secret scanning (alerts) and, if available, push protection
  - Dependabot alerts (and security updates)
  - Branch protection / rulesets and required reviews for risky changes
  - CODEOWNERS for `.github/workflows/**` and other security-critical paths
- When a change touches workflows, auth, or secret handling, require extra review and be explicit about risk.

### If a secret leaks (incident playbook)
1. **Rotate/Revoke immediately** (this is the primary mitigation).
2. Identify blast radius: which systems used the credential and where it was copied.
3. Remove/replace usages in code/config and redeploy.
4. Assess whether history rewrite is necessary (often rotation is sufficient; rewriting history has major side effects).
5. Add prevention:
   - `.gitignore` updates
   - pre-commit secret scanning (e.g., detect-secrets / gitleaks / trufflehog)
   - CI secret scanning gates

### "Vibecoding" guardrails (fast prototyping without leaks)
When rapidly iterating:
- default to env vars + `.env.example`
- avoid copying real credentials into prompts, issues, or sample snippets
- keep logs minimal; don't print request headers, env dumps, or full exception objects that may contain secrets

### References (for maintainers)
- GitHub Docs: Using secrets in GitHub Actions
  - https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions
- GitHub Docs: Secure use reference (Actions hardening)
  - https://docs.github.com/en/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions
- GitHub Docs: `GITHUB_TOKEN` least privilege
  - https://docs.github.com/en/actions/security-guides/automatic-token-authentication
- GitHub Docs: Mask values in logs (`::add-mask::`)
  - https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#masking-a-value-in-a-log
- GitHub Docs: About secret scanning
  - https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning
- GitHub Docs: About push protection
  - https://docs.github.com/en/code-security/secret-scanning/introduction/about-push-protection
- GitHub Docs: Best practices for preventing data leaks
  - https://docs.github.com/en/code-security/getting-started/best-practices-for-preventing-data-leaks-in-your-organization
- GitHub Docs: Removing sensitive data from a repository (git-filter-repo)
  - https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository
- GitHub Docs: Managing personal access tokens (fine-grained PATs)
  - https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens
- GitHub Docs: Dependabot alerts
  - https://docs.github.com/en/code-security/dependabot/dependabot-alerts/about-dependabot-alerts