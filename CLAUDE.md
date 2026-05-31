# CLAUDE.md — HOF Hub (Staff Portal)

Central entry point for all HOF staff-facing tools. A single URL that presents two app cards — Broker Fact Find and HOF Learning Hub — so staff always know where to start.

**Live URL:** `https://hof-hub.vercel.app`
**GitHub:** `GoldenMonkey4100/hof-hub` (not yet connected — deployed via Vercel CLI directly)
**Local path:** `C:\Users\ck\OneDrive\Documents\House of Finance AI Brain\05 - HOF Hub\`

---

## Stack
Single `index.html` — no framework, no build step, no dependencies. Vercel deploys it as a static site. No `package.json`.

---

## Files
```
05 - HOF Hub/
├── index.html     ← entire app: HTML + embedded CSS + JS (auth when added)
├── vercel.json    ← cleanUrls: true, trailingSlash: false
└── .gitignore
```

---

## Cards
| Card | Links to | Description shown |
|---|---|---|
| Broker Fact Find | `https://hof-fact-find.vercel.app/` | Complete a client loan application |
| HOF Learning Hub | `https://hof-lms.vercel.app/dashboard` | Access staff training modules |

Cards open in a new tab (`target="_blank"`).

---

## Branding
Matches Broker Fact Find dark luxury aesthetic:
- Header: `#12110D` background, `1px solid rgba(203,178,107,0.18)` border, HOF logomark + wordmark
- Cards: white, `border-left: 3px solid #CBB26B`, gold-tinted borders
- CTA buttons: `#12110D` bg, `#CBB26B` gold text, Montserrat uppercase
- Page bg: `#F5F4F2` porcelain
- Fonts: Montserrat (headings/labels) + Open Sans (body) via Google Fonts

---

## Planned: Microsoft Auth Gate
Microsoft account login via MSAL.js (CDN, no backend needed).

**Requires Azure AD app registration first:**
- portal.azure.com → Azure Active Directory → App registrations → New registration
- Platform: Single-page application (SPA)
- Redirect URI: `https://hof-hub.vercel.app`
- Account type: Single tenant (HOF org only)
- Get: **Client ID** + **Tenant ID**

Auth flow: redirect (not popup) — works on all browsers including Safari/iOS.
Two views: `#view-login` (unauthenticated) and `#view-portal` (authenticated cards).
Post-login: user's display name shown in header, sign-out button.

---

## Deployment
```bash
vercel --prod   # from inside 05 - HOF Hub/ directory
```
No GitHub auto-deploy connected yet. Manual deploy via CLI.
