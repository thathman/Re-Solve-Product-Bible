# Re:Solve Authentication Expansion

Status: PRODUCT REQUIREMENT / ARCHITECTURE ROADMAP

This document records the approved authentication expansion without implementing it yet.

## Supported sign-in and verification methods

Re:Solve will support:
- email + password;
- email magic link;
- Google OAuth;
- GitHub OAuth;
- passkeys / WebAuthn when the production relying-party hostname is stable;
- TOTP as a second factor / MFA mechanism;
- ALTCHA as the application abuse/CAPTCHA layer on appropriate auth entry points.

TOTP is not a replacement first-factor login method. It upgrades a conventional authenticated session to the stronger MFA assurance level.

## Invite-oriented account policy

Re:Solve remains invite-oriented. Enabling OAuth or passwordless methods must not silently turn the product into public signup.

Before social/passwordless expansion is enabled, preserve one of these server-controlled signup constraints:
- disable new-user signup so only pre-existing/invited Auth Users can sign in; and/or
- use a reviewed Before User Created auth hook tied to the future invitation/allowlist model.

Browser metadata is never authorization evidence. Admin access still requires server-authoritative staff access. Portal access still requires server-authoritative organisation membership.

## ALTCHA

ALTCHA should be self-hosted and server-verified. Treat it as an abuse-control layer, not as authentication or authorization evidence and not as a replacement for Supabase Auth rate limiting.

Apply it where it meaningfully limits automation, especially magic-link/OTP sends, password-reset requests, and risk-based/repeated password attempts. Do not force CAPTCHA onto passkey/WebAuthn ceremonies merely for consistency.

## TOTP / MFA policy direction

Use Supabase Auth MFA/TOTP rather than a parallel application-owned TOTP implementation.

Policy direction:
- staff/Admin: require AAL2 once enrollment/recovery UX exists;
- client Portal: allow TOTP enrollment and support later step-up requirements for sensitive actions;
- do not expose or log TOTP enrollment secrets outside the transient enrollment UX.

## Passkeys

Supabase Auth passkey support is currently experimental. Re:Solve may support it as an opt-in first-factor login method, but should not make it the sole recovery path while the API remains experimental.

Do not enroll production passkeys against temporary Lovable/dev hostnames. Pick the final production WebAuthn RP ID/origins first and keep them stable.

## Google and GitHub

Use native Supabase OAuth flows. Preserve safe internal returnTo handling and the existing PKCE/callback architecture.

OAuth must not grant Admin or Portal authorization by itself. Existing staff and organisation-membership gates remain authoritative.

## WhatsApp authentication

WhatsApp sign-in is desirable as a future phone-possession authentication option, but Baileys is NOT approved as the canonical identity root of trust.

Baileys remains suitable for the separate Re:Solve WhatsApp messaging/connector capability, not for foundational account authentication.

Preferred authentication architecture is an official WhatsApp Business Platform authentication/OTP flow, mapped into a reviewed Re:Solve/Supabase identity flow. This requires a separate design because Supabase does not expose WhatsApp as a native OAuth identity provider.

Do not implement a custom WhatsApp-issued Supabase session, service-role shortcut, or Baileys OTP bridge without a separately reviewed auth design.

## Sequencing

Implement in small supervised slices after the current client visual rollout:
1. ALTCHA challenge/verification boundary + auth rate-limit review;
2. magic-link first-factor flow;
3. Google + GitHub OAuth under invite-only policy;
4. TOTP enrollment/challenge + AAL2 enforcement policy;
5. passkey opt-in after production RP ID is fixed;
6. WhatsApp authentication architecture preflight, favoring official WhatsApp Business Platform over Baileys;
7. security-settings UI for identity linking, factor management, passkeys and recovery.

No auth expansion slice may weaken F1A/F1B session handling, F3A Admin authorization, F3B Portal authorization, F3C exact-organisation revalidation, CSRF, RLS, service-role quarantine, or raw-error/secret logging rules.
