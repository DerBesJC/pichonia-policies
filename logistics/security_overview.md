# Security Overview – Logistics
_Last updated: 2025-11-04_

## 1. Objectives
Protect user data, prevent abuse, and meet store/compliance expectations with pragmatic, least-privilege controls.

## 2. Data in Scope
- **Account data:** name, email/phone, role (customer/owner/driver).
- **Operational data:** job requests, assignments, timestamps, location traces (where enabled).
- **Billing artifacts:** last 4 of card (via processor), invoices, refunds (metadata only).

## 3. Architecture & Storage
- **Auth & Identity:** Firebase Authentication (email/phone/OTP).
- **Data:** Firestore/RTDB (role-scoped collections), access via security rules.
- **Media:** Firebase Storage with per-object rules.
- **Secrets:** platform keychains + environment-scoped configs (no secrets in code).

## 4. Transport & Encryption
- **In transit:** HTTPS/TLS 1.2+ everywhere.
- **At rest:** Provider-managed encryption (Firestore/Storage).
- **Tokens:** short-lived where possible; signed URLs for media.

## 5. Access Control
- **RBAC:** roles (customer, truck owner, driver, admin).
- **Principle:** least privilege; deny by default in rules.
- **Owner↔Driver:** owner can only view/assign to own drivers.

## 6. Logging & Monitoring
- **Crash & Telemetry:** Firebase Crashlytics + minimal custom logs.
- **Retention:** telemetry 90–180 days; audit trails 12–24 months where required.
- **PII in logs:** prohibited by convention + lint checks where applicable.

## 7. Payments
- **Processor:** Stripe (hosted UIs; no full PAN stored by Pichonia).
- **Artifacts:** charges/receipts retained up to 7 years (tax/audit).

## 8. Location & Maps
- **Provider:** Google Maps Platform.
- **Minimization:** only active-job location; no background tracking unless user-enabled.

## 9. Secure Development
- **Repo:** branch protection, code review.
- **Mobile:** release signing, store-only builds.
- **Dependencies:** pinned versions; supply-chain checks.

## 10. Incident Response
- **Triage window:** acknowledge within 24–72h depending on severity.
- **Containment:** rotate keys, revoke tokens, hotfix rules.
- **Notification:** as legally required and appropriate.

## 11. Contact
security@pichonia.com · info@pichonia.com
