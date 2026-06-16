# Jones Booking Platform App V3.3 Audit and HTTPS Integration Plan

## Prompt

You are Claude Code. Execute this plan exactly.

Important correction:
- Do not treat the booking system as only a "Booking API."
- The correct target is the separate Booking Platform Application.
- The booking platform may contain backend routes, API endpoints, admin screens, database/storage logic, booking workflow logic, notification logic, and deployment configuration.
- The barbershop website is a separate project that connects to the booking platform.
- The connection between the website and the booking platform must be discovered before changing deployment settings.

Primary objective:
Apply the Project Starter Kit v3.3 workflow to the Booking Platform Application as its own software package, then connect it safely to the Jones Barbershop website over HTTPS.

Do not deploy or change production until the booking platform has gone through:
1. package discovery
2. v3.3 audit-only pass
3. quality-gate review
4. local verification
5. HTTPS production integration planning
6. approved deployment
7. website connection update
8. end-to-end verification

---

## Correct Mental Model

There are at least two separate systems:

```text
Jones Barbershop Website
- public marketing site
- contains the booking UI or booking entry point
- may contain a data-api-url, booking form, embed, script, or redirect
- should not contain backend secrets

Booking Platform Application
- separate application/package
- handles booking workflow
- may expose an API
- may have an admin dashboard
- may store booking data
- may send notifications
- may run as Node/Express, Next.js, Flask, Laravel, static + serverless, or something else
- must be audited as its own app before production use
```

The phrase "booking API" should only be used if the audit confirms that the platform exposes an API endpoint that the website calls.

---

## Non-Negotiable Rules

1. Start with read-only audit mode.
2. Do not modify files until the audit report is complete.
3. Do not assume the booking platform is only an API.
4. Do not assume the platform uses PM2.
5. Do not assume port 3001 is correct.
6. Do not assume Node.js unless package files prove it.
7. Do not expose public raw HTTP for production.
8. Production connection must use HTTPS.
9. Do not commit `.env`, secrets, credentials, tokens, private keys, customer data, or database dumps.
10. Do not blindly merge v3.3 files into the booking platform app.
11. Treat v3.3 as a workflow overlay first.
12. Stop and ask for confirmation when production values are ambiguous.
13. Use the workflow: check → fix → verify → commit → push.

---

## Required Discovery Questions

Before making changes, answer these from the actual files:

1. Where is the Booking Platform Application located?
2. Is it inside the barbershop repo, beside it, or in a separate repo?
3. What framework/runtime does it use?
4. Does it have its own `package.json`, `requirements.txt`, `composer.json`, `Dockerfile`, or other app manifest?
5. Does it have its own Git history?
6. Does it have its own README/docs?
7. How does the barbershop website currently connect to it?
8. Is the connection a form POST, API call, script include, iframe/embed, redirect, or something else?
9. Does the booking platform have an admin interface?
10. Does it use a database or file storage?
11. Does it send email/SMS notifications?
12. Does it already have environment variables?
13. Does it already have deployment instructions?
14. Does it already have production hosting?
15. Does it already have HTTPS configured?

---

## Phase 0 — Preflight Safety Check

From the current workspace:

```bash
pwd
git status
git branch --show-current
git log --oneline -8
```

Confirm:
- The current repo is known.
- Previous barbershop website audit changes are committed and pushed.
- The working tree is clean, or only this plan file is uncommitted.

If the working tree is dirty, report the changed files and stop.

---

## Phase 1 — Locate the Booking Platform Application

Search the current repo and nearby folders for likely booking platform files.

From the barbershop repo root:

```bash
find . -maxdepth 6 -type f \( \
  -name "package.json" -o \
  -name "requirements.txt" -o \
  -name "pyproject.toml" -o \
  -name "composer.json" -o \
  -name "Dockerfile" -o \
  -name "docker-compose.yml" -o \
  -name "server.js" -o \
  -name "app.js" -o \
  -name "index.js" -o \
  -name ".env.example" -o \
  -name "ecosystem.config.*" \
\) -print
```

Search for booking-related terms:

```bash
grep -Rni "booking\|appointment\|schedule\|calendar\|availability\|customer\|barber\|service\|data-api-url\|api-url\|iframe\|embed\|form" . \
  --exclude-dir=node_modules \
  --exclude-dir=.git \
  --exclude-dir=dist \
  --exclude-dir=build
```

If the booking platform is outside the current repo, identify its path and stop for confirmation before operating on it.

Output a discovery report:

```text
Booking Platform Discovery Report
- App location:
- Separate repo or same repo:
- Framework/runtime:
- App manifest:
- Current start command:
- Current build command:
- Current test command:
- Current deployment assumptions:
- Website connection method:
- Known blockers:
- Unknowns requiring user confirmation:
```

Stop after this report if the app location is ambiguous.

---

## Phase 2 — Treat Booking Platform as Its Own Project

If the booking platform is a separate repo:

```bash
cd BOOKING_PLATFORM_APP_DIR
git status
git checkout -b workflow/v3.3-booking-platform-audit
```

If the booking platform is inside the barbershop repo:
- Do not split it yet.
- Report the structure.
- Recommend whether it should remain a subfolder or become a separate repo.
- Continue only if the structure is safe.

If it is not under Git:
- Stop and ask whether to initialize Git.
- Do not proceed without a rollback point.

---

## Phase 3 — Add V3.3 as a Contained Reference Only

If v3.3 is not already present in the booking platform app, add it as a contained reference folder:

```text
_project-starter-kit-v3.3/
```

Correct:

```text
booking-platform/
├── app files...
├── README.md
└── _project-starter-kit-v3.3/
```

Do not blindly overwrite:

```text
CLAUDE.md
CONTEXT.md
README.md
docs/
prompts/
.claude/
```

If equivalent files already exist, the audit must compare and recommend merges later.

Commit only if appropriate:

```bash
git add _project-starter-kit-v3.3
git commit -m "chore: add v3.3 workflow reference for booking platform"
```

If the repo policy should avoid storing the full reference kit, stop and recommend an alternative.

---

## Phase 4 — Booking Platform V3.3 Audit-Only Pass

Run the v3.3 workflow against the booking platform in audit-only mode.

Rules:
- Do not modify files.
- Do not rename files.
- Do not delete files.
- Do not restructure.
- Do not deploy.
- Do not edit the barbershop website yet.
- Do not run auto-fixes.

Audit report must cover:

1. Application purpose
2. Package structure
3. Framework/runtime
4. Entry points
5. Public routes/pages
6. Backend routes/endpoints if present
7. Admin UI if present
8. Booking workflow
9. Data model/storage
10. Environment variables
11. Secret handling
12. Authentication/authorization if present
13. Input validation
14. Error handling
15. Logging
16. Email/SMS/notification behavior
17. CORS or cross-origin behavior if relevant
18. Build/start/test scripts
19. Deployment readiness
20. HTTPS readiness
21. Documentation gaps
22. Test gaps
23. Security risks
24. Production blockers
25. Exact proposed file changes
26. Files that should not be touched

Stop after the audit report.

---

## Phase 5 — Implement Minimum Quality-Gate Fixes

After the audit, implement only required fixes needed to make the booking platform safe and deployable.

Possible fixes:
- `.gitignore`
- `.env.example`
- README deployment section
- health/status endpoint if the app has a backend service
- configurable production URL/origin
- configurable port only if applicable
- safe CORS allowlist only if cross-origin requests exist
- validation for booking form inputs
- clear error responses
- production start script
- PM2 ecosystem file only if the app is a Node service and PM2 is selected
- Docker files only if Docker is selected
- deployment notes
- manual verification checklist

Do not overbuild.

Commit quality-gate changes only after review:

```bash
git status
git diff --stat
git add .
git commit -m "chore: pass v3.3 quality gate for booking platform"
```

Before committing, ensure no secrets or customer data are staged.

---

## Phase 6 — Local Verification

Run the commands discovered by the audit.

Examples only:

```bash
npm install
npm run lint
npm test
npm run build
npm start
```

or:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python app.py
```

or use the app's actual documented workflow.

Verify:
- App starts locally.
- Booking workflow works with fake test data.
- Admin UI works if present.
- Validation works.
- Error states are safe.
- No secrets are printed.
- No real customer data is used.

If the platform exposes a health route, test it:

```bash
curl -i http://127.0.0.1:LOCAL_PORT/health
```

If it does not expose a backend route, do not invent one unless the audit recommends it as a deployment requirement.

---

## Phase 7 — Determine Website-to-Platform Connection Method

Return to the barbershop website repo.

Find how the website connects to the booking platform:

```bash
grep -Rni "data-api-url\|booking\|appointment\|schedule\|iframe\|embed\|src=\|action=\|fetch\|axios\|XMLHttpRequest" . \
  --exclude-dir=node_modules \
  --exclude-dir=.git \
  --exclude-dir=dist \
  --exclude-dir=build
```

Classify the connection as one of:

```text
A. Website posts directly to backend endpoint
B. Website loads booking platform via iframe/embed
C. Website links/redirects to booking platform
D. Website loads a booking widget script
E. Website and booking platform are served from same app
F. Unknown/other
```

Do not edit the website until the connection method is clear.

---

## Phase 8 — HTTPS Production Integration Plan

Create the production integration plan based on the actual app type.

Possible patterns:

### Pattern A — Same domain path

```text
https://barbershop-domain.com/booking
https://barbershop-domain.com/api
```

Best when the platform can live behind the same domain and reverse proxy.

### Pattern B — Booking subdomain

```text
https://booking.barbershop-domain.com
```

Best when the booking platform has its own UI/admin app.

### Pattern C — API subdomain

```text
https://api.barbershop-domain.com
```

Only appropriate if the website calls backend API endpoints directly and there is no separate booking UI.

### Pattern D — External hosted booking app URL

```text
https://booking-platform-domain.com
```

Only appropriate if the booking platform is intentionally hosted as a separate public product.

Choose based on actual architecture, not assumption.

Production must use HTTPS.

---

## Phase 9 — VPS / Hosting Preflight

If deploying to the VPS, inspect first:

```bash
ssh VPS_USER@VPS_HOST
```

Then:

```bash
hostname
whoami
pwd
node -v || true
npm -v || true
python3 --version || true
pm2 -v || true
docker --version || true
which nginx || true
which caddy || true
which apache2 || true
sudo systemctl status nginx --no-pager || true
sudo systemctl status caddy --no-pager || true
sudo systemctl status apache2 --no-pager || true
sudo ufw status || true
sudo ss -tulpn | grep -E ':80|:443|:3000|:3001|:8000|:8080' || true
```

Determine:
- Existing reverse proxy
- Existing TLS method
- Existing website deployment path
- Existing app deployment convention
- Runtime availability
- Whether Docker or PM2 is preferred
- Whether selected ports are already in use

Stop if the hosting stack is ambiguous.

---

## Phase 10 — Deploy Booking Platform

Deploy according to the audited app type.

Do not assume PM2 unless:
- the app is a long-running Node service, and
- the VPS uses PM2 or PM2 is approved.

Do not assume port 3001 unless:
- the app config already uses it, or
- the user approves it, or
- the deployment plan selects it as an internal port with no conflict.

Possible deployment methods:
- Git pull
- rsync
- Docker Compose
- PM2
- systemd service
- static build served by reverse proxy
- existing VPS deployment convention

The deployment method must be documented in the final report.

---

## Phase 11 — Configure HTTPS Reverse Proxy

Public access must use HTTPS.

Do not expose raw backend ports publicly.

Back up existing proxy config before editing.

Valid public URL examples:

```text
https://SITE_DOMAIN/booking
https://booking.SITE_DOMAIN
https://SITE_DOMAIN/api
https://api.SITE_DOMAIN
```

Invalid production target for the website:

```text
http://VPS_IP:3001
```

Only use internal HTTP between the reverse proxy and app:

```text
http://127.0.0.1:INTERNAL_PORT
```

Validate proxy config before reload.

Examples:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

or:

```bash
sudo caddy validate --config /etc/caddy/Caddyfile
sudo systemctl reload caddy
```

---

## Phase 12 — Update Barbershop Website Connection

Only after the production booking platform URL works over HTTPS:

- Update `data-api-url` only if the website uses direct API calls.
- Update booking link only if the website redirects.
- Update iframe `src` only if embedded.
- Update widget script URL only if script-based.
- Update no frontend URL if reverse proxy makes the route same-origin transparently.

Use the actual connection method discovered earlier.

Check the diff before committing:

```bash
git diff --stat
git diff
```

---

## Phase 13 — End-to-End Verification

Test from the browser:

1. Open the live barbershop website.
2. Load the booking UI.
3. Submit fake test booking data.
4. Confirm the booking platform receives the request.
5. Confirm validation works.
6. Confirm success state works.
7. Confirm failure state works.
8. Confirm admin/storage/notification behavior if applicable.
9. Confirm browser console has no CORS errors.
10. Confirm browser console has no mixed-content errors.
11. Confirm network requests use HTTPS.
12. Confirm no request goes to raw `http://VPS_IP:PORT`.

Do not use real customer data.

---

## Phase 14 — Commit and Push

Booking platform repo/package:

```bash
cd BOOKING_PLATFORM_APP_DIR
git status
git add .
git commit -m "chore: complete v3.3 gate for booking platform"
git push -u origin workflow/v3.3-booking-platform-audit
```

Website repo/package if changed:

```bash
cd WEBSITE_REPO_DIR
git status
git add .
git commit -m "deploy: connect website to HTTPS booking platform"
git push -u origin deploy/connect-booking-platform-https
```

If both are in one repo, create one clear commit after reviewing combined diff.

Do not push to main unless explicitly approved.

---

## Phase 15 — Final Report

Produce a final report:

```text
Final Booking Platform Integration Report

1. Booking platform location:
2. Separate repo or same repo:
3. Framework/runtime:
4. Connection method:
5. V3.3 audit summary:
6. Quality-gate fixes made:
7. Local verification results:
8. Deployment method:
9. VPS/hosting path:
10. Process manager/container/service:
11. Reverse proxy:
12. HTTPS public URL:
13. Website files changed:
14. Final website connection value:
15. End-to-end booking test result:
16. Browser console result:
17. Remaining risks:
18. Rollback steps:
19. Branches:
20. Commit hashes:
```

Do not claim success unless the live barbershop website connects to the booking platform successfully over HTTPS.

---

## Rollback Requirements

Document rollback based on the actual deployment method.

Minimum rollback items:
- Stop app process/container/service.
- Restore previous reverse proxy config.
- Revert website connection change.
- Revert booking platform changes if needed.
- Confirm live website is back to previous working state.

---

## Success Criteria

The work is complete only when:

- The booking platform app has been identified correctly.
- It has been audited as its own app/package.
- V3.3 workflow has been applied as an overlay, not blindly merged.
- Required quality-gate fixes are complete.
- The app runs locally.
- The app is deployed using the correct hosting method.
- Public access uses HTTPS.
- The barbershop website connects to the booking platform correctly.
- No raw public HTTP backend URL is used by the website.
- End-to-end fake booking test passes.
- Browser console has no CORS or mixed-content errors.
- No secrets are committed.
- Changes are committed and pushed.
- Final report is produced.
