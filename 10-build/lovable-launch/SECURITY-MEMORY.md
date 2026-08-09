# Re:Solve Security Memory

This is the concise security source of truth for Lovable/project memory. It complements the fuller Product Bible architecture and does not replace slice-specific acceptance criteria.

## Authority boundaries
- Authentication, staff access, organisation access, roles, permissions and capabilities are server-authoritative.
- Browser route guards, route context, localStorage, cookies and UI state are UX/context only and never sufficient authorization evidence.
- Every private server function/route independently authenticates and authorizes the current request.
- `/admin` requires active staff access. Portal access requires active organisation membership. Exact organisation-scoped operations revalidate that exact organisation server-side.
- `rs_portal_org` is an untrusted UUID-only context pointer, never authorization evidence.

## Supabase / database
- Normal user data access uses caller-scoped Supabase plus RLS and least privilege.
- Service-role/private credentials are server-only and are never a normal application authorization path.
- Generated `supabaseAdmin` remains quarantined unless a separately reviewed privileged server boundary explicitly adopts an admin operation.
- RLS and grants are version-controlled. `SECURITY INVOKER` is the default; `SECURITY DEFINER` requires a narrow, documented, reviewed justification.
- Do not create broad bypass policies, generic recursion workarounds or client-controlled authorization metadata.

## Auth
- Current account model is invite-oriented; there is no public registration.
- Future Google/GitHub linking must attach to an existing invited/authenticated user and must not create a Re:Solve account by itself.
- Auth callbacks/redirects use the canonical safe internal redirect validator.
- Password, recovery, provider and validation failures shown to users must be generic/provider-neutral; never surface raw provider errors.
- Tokens, sessions, recovery codes, factor secrets and provider secrets are never logged.

## Request / mutation safety
- Preserve explicit `createCsrfMiddleware` in `src/start.ts`.
- Consequential server boundaries require runtime input validation.
- Consequential mutations should ultimately pass through the canonical Action Registry/equivalent audited mutation boundary once that foundation exists.
- Do not trust browser-supplied role, capability, organisation or resource-ownership claims.

## Vault / secrets
- Vault secrets and durable credentials never enter browser storage, analytics, search indexes, notifications, general logs, non-Vault surfaces or caches.
- QR codes may contain only signed, scoped, short-lived references/tokens; never raw secrets or durable credentials.
- Secret-reveal flows require explicit authorization and later step-up controls where specified by the product architecture.

## Logging / errors
- Never log raw auth/database/provider/Zod/access errors when they may contain sensitive request or identity detail.
- Never log tokens, cookies, sessions, passwords, secret values or privileged credentials.
- Use stable user-facing/internal error messages and fixed diagnostic labels where logging is necessary.

## PWA / offline / browser persistence
- Cache Storage is not a trusted private-data store.
- Service-worker caching uses a positive allowlist only. Unknown requests are network-only.
- The foundation public cache may contain only explicitly approved public static assets such as the offline page, manifest, favicon and PWA icons.
- Never cache authenticated/private route HTML, server-function/RPC responses, Supabase/API responses, auth/recovery callbacks, organisation/profile/project/property/billing/support data, notifications, Àríyá/Chatwoot content, Vault data, tokens or session material.
- Navigation may use network-first with a generic cached offline fallback, but successful navigation responses are never written to Cache Storage.
- No offline mutations, background sync, private IndexedDB persistence or offline business-data access exists unless separately designed and security-reviewed.
- Service workers register only in production.
- A waiting service worker may activate via explicit `SKIP_WAITING` only after the user chooses to refresh/update. `controllerchange` must never force a reload unless that reload was explicitly user-requested.

## Local browser preferences
- localStorage may hold non-sensitive presentation preferences such as theme and movable Àríyá launcher position.
- Never store identity, organisation authorization, permissions, secrets or conversation/business payloads in those preference keys.

## Development preview
- `import.meta.env.DEV` may bypass Admin/Portal route-level UX redirects for visual preview only.
- DEV preview never weakens server authorization, RLS, CSRF or private server-function checks.
- No query-string, cookie, localStorage or production-enabled auth bypass is allowed.

## AI / support boundary
- Àríyá is Re:Solve's own AI and remains inside Re:Solve.
- Re:Solve human escalation eventually routes to the dedicated Re:Solve-support Chatwoot inbox where Captain is disabled.
- Property/site-specific Chatwoot inboxes may use Captain independently when configured for that property's support; this never powers or replaces Àríyá.

## Supply chain / portability
- Prefer standard, self-hostable dependencies and APIs. Lovable is the build environment, not a production runtime dependency.
- New dependencies require review for necessity, maintenance, licensing and security impact.
- No production secret should be required for build/lint/typecheck/CI.

If a future prompt conflicts with this file, stop and resolve the conflict explicitly rather than silently weakening the security boundary.
