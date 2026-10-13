## 18. Security

- React escapes output by default; avoid `dangerouslySetInnerHTML` (sanitize with DOMPurify if unavoidable). Validate URLs from users (block `javascript:` links).
- **Never trust the client:** enforce authorization on the server; hiding a button is not security.
- Tokens: prefer httpOnly, Secure, SameSite cookies over `localStorage` (which any XSS can read). Understand CSRF when using cookies.
- Set security headers: Content-Security-Policy, `frame-ancestors` (clickjacking), `X-Content-Type-Options`, HSTS. Understand CORS (it is enforced by browsers, configured on the server).
- Never put secrets in the frontend bundle; anything in `VITE_*` or `NEXT_PUBLIC_*` env vars is public.
- **Supply chain:** commit lockfiles, review new dependencies (maintenance, downloads, scripts), audit regularly (`npm audit`, GitLab dependency scanning), consider disabling install scripts for untrusted packages.
- Protect against open redirects, unsafe `postMessage`, unsafe file uploads, and leaking PII into logs or analytics.
- Use GitLab SAST, secret detection, and dependency scanning templates in CI.
- Do not roll your own auth or crypto.
