# Security Overview – Trading AI
_Last updated: 2025-11-04_

## 1. Objectives
Safeguard account data, protect API tokens, and ensure integrity of analytics/backtests.

## 2. Data in Scope
- **Account:** name, email, password hash, subscription status.
- **Telemetry:** run counts, feature flags, error traces (no PII).
- **Integrations:** broker/data provider tokens (optional; encrypted).

## 3. Architecture & Storage
- **Auth:** platform auth (email/OTP/password).
- **App/Data:** managed cloud (DB + object storage), environment-scoped configs.
- **Secrets:** stored in managed secret stores; never committed to code.

## 4. Transport & Encryption
- **HTTPS/TLS 1.2+** everywhere.
- **At rest:** provider-managed encryption.
- **Token handling:** minimum scopes, revocable, rotated on suspicion.

## 5. Access Control
- **RBAC:** user, admin/support (restricted tools).
- **Data boundaries:** user-scoped datasets; no cross-tenant leakage.

## 6. Logging & Monitoring
- **Telemetry:** minimal + aggregated; no trading credentials in logs.
- **Retention:** 90–180 days telemetry; 12–24 months audit as needed.

## 7. Payments
- **Processor:** Stripe; no full PAN stored by Pichonia.
- **Artifacts:** invoices/receipts retained up to 7 years (tax/audit).

## 8. Integrations (Market/Broker)
- **Principle:** least privilege; read-only where possible.
- **Revocation:** users can revoke any time; we delete tokens on revocation/deletion.

## 9. Secure Development
- **Code:** review + CI checks; dependency scanning.
- **Releases:** environment separation (dev/int/prod); feature flags.

## 10. Incident Response
- **Acknowledge:** ≤ 72h based on severity.
- **Contain:** revoke tokens, rollback builds, rotate keys.
- **Notify:** when required by law and appropriate to risk.

## 11. Contact
security@pichonia.com · info@pichonia.com
