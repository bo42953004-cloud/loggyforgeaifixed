# Validation notes

Verified on the fixed package (Node 22, `npm install` with the committed `.npmrc`):

- `npm run typecheck` — passes with no errors.
- `npm run lint` — 0 errors (a few non-blocking warnings remain).
- `npm run build` — production build succeeds (this is what Vercel runs).
- End-to-end test against a real PostgreSQL: register, duplicate email, invalid referral code, session cookie,
  wrong-password login, correct login, device-binding rule, admin login and admin session — all returned the
  expected JSON responses.
- With `DATABASE_URL` missing, register/login now return a readable JSON error instead of an empty response.

Not tested: live Daraja/M-Pesa payments (needs your real Safaricom credentials and a public callback URL).
Follow the Sandbox checklist in `DEPLOY.md` before taking real payments.


## Upgrade validation notes
- The project ZIP was inspected and its archive integrity verified.
- Source changes include admin subscription grants, custom plan configuration, subscription-health colour calculation, optional Neon Glass styling, branded login loader and lower-cost mobile animation settings.
- A full TypeScript/build run was not possible in this packaging environment because project dependencies are not installed and registry installation timed out. Run `npm install`, `npm run typecheck`, and `npm run build` before deploying. The lockfile root dependency list includes `@vercel/blob`; `npm install` must refresh the resolved package graph.
- Daraja production transactions were not tested. Existing credentials remain encrypted in your own database and are not present in this ZIP. Test with the existing Sandbox/Production configuration appropriate to your Safaricom account before accepting live payments.
