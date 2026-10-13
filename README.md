# MAKCISS CAPITAL — Marketplace MVP prototype

Mobile-first storefront prototype for a future local-first marketplace in **Mali and Spain**. Cross-border sales are explicitly postponed until payment, logistics, tax/customs, returns, and legal requirements have been verified.

## Current status

**Prototype only — not production-ready.** The current branch replaces the generic Svelte/Vite starter screen with an interactive storefront to test the user journey on a phone.

### Implemented in this prototype
- Switch between the Spain (EUR) and Mali (XOF/FCFA) demo catalogues.
- Search and category filters.
- Add/remove demo items and calculate a local cart subtotal.
- Demo checkout path that clearly states no order or payment is sent.
- Seller entry point explaining that onboarding is not connected.
- Responsive layouts for mobile and desktop.
- Accessibility labels for key controls and reduced-motion support.

### Not implemented (do not treat as live)
- Authentication, seller verification, roles, or admin console.
- Real product inventory, seller listings, order persistence, or delivery tracking.
- Payment provider, seller payouts, commissions, refunds, or chargeback handling.
- Notifications, customer support workflow, fraud controls, or production audit logs.
- Legal documents, tax handling, GDPR workflows, Spanish/Malian consumer disclosures, or cross-border customs.
- Real product images, verified merchants, or confirmed product availability. All catalogue items/prices are illustrative.

## Local development

Requires a current Node.js version compatible with Vite 8.

```bash
npm install
npm run dev
npm run build
npm run preview
```

**Dependency note:** the starter repository's committed `package-lock.json` was out of sync with `package.json` when first checked. Use `npm install` to reconcile dependencies for now. Before production, regenerate and commit a verified lockfile, then restore `npm ci` in CI for deterministic installs.

## Launch strategy

1. Validate this demo on an iPhone and correct the mobile UX.
2. Define the first local operating zone in Mali and Spain, verified sellers, allowed product categories, delivery service, returns, and support.
3. Select the legal business model and payment providers only after written confirmation of supported merchant countries, onboarding/KYC, marketplace commissions, payouts, refunds and chargebacks. MAKCISS CAPITAL must not hold seller funds unless an appropriately regulated setup has been verified.
4. Add a backend and database with server-side authorization, order state transitions, audit trail, idempotent payment webhooks, and tests.
5. Run controlled test orders in each market before enabling live payments.
6. Consider cross-border sales only after the local flows are reliable and customs/tax/shipping requirements are documented.

## Important security rule

Never put payment secrets, service-role database keys, private API keys, or provider credentials in client-side Svelte code or Git. Use server-side environment variables and a backend with least-privilege access.

## Working branch

`feat/makciss-local-first-marketplace`
