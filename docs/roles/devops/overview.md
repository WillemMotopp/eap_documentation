# DevOps Engineer — Role Overview

## Role Overview

### What is a DevOps Engineer?

The DevOps Engineer is **responsible for the reliability, repeatability, and speed of the software delivery process** — from code commit to running application.

**You are NOT:**
- ❌ A developer who writes application features
- ❌ The person responsible for fixing application bugs
- ❌ "The person who knows how computers work" — DevOps is a discipline, not a catch-all
- ❌ Working alone in isolation — DevOps enables the whole team

**You ARE:**
- ✅ The owner of the CI/CD pipeline and deployment process
- ✅ The guardian of the infrastructure (VPS, Nginx, SSL, firewall)
- ✅ The person who makes deployments fast, reliable, and repeatable
- ✅ The team's partner for anything involving environments, secrets, and deployment

### Core Responsibility

**One sentence:** You ensure the team can **build, test, and deploy** software reliably — by owning the pipeline, maintaining the VPS infrastructure, and making the deployment process transparent and reproducible.

---

## Key Responsibilities

### 1. CI/CD Pipeline Ownership

**You own all GitHub Actions workflows across all 4 repositories.** This means:

**Building:**
- Pipelines run automatically on every pull request (build, lint, test)
- Developers get fast feedback — broken builds are caught before merge
- All 4 repos have working pipeline files in `.github/workflows/`

**Testing:**
- Automated tests are wired into the pipeline — they run without anyone pressing a button
- Frontend pipelines run type checks and unit tests
- Backend pipelines run pytest (with coverage reporting)
- QA repo pipelines trigger end-to-end tests against the test environment

**Deploying:**
- Deployment pipelines trigger automatically on merge to `dev` or `main`
- Deployment to `prod` is a manual, gated action (after Sprint Review sign-off)
- Pipeline history is the audit trail — every deployment is recorded in GitHub Actions

**Maintaining:**
- When a pipeline breaks due to a code change, you help diagnose and fix it
- Pipeline files are kept up-to-date as the application evolves
- New pipeline steps (e.g., adding a linter, adding a test step) are introduced incrementally via pull request

### 2. VPS & Infrastructure Management

**You manage the TransIP VPS.** This is the production server where the application runs.

**Nginx (Reverse Proxy):**
- Configure Nginx to route traffic to the correct application service
- Set up virtual hosts for each environment (dev, test, prod)
- Ensure all HTTP traffic redirects to HTTPS
- Monitor Nginx access and error logs for issues

**SSL Certificates (Certbot / Let's Encrypt):**
- All environments must run on HTTPS — no exceptions
- Certbot handles certificate issuance and renewal
- Automated renewal via cron job — you set this up and verify it works
- Monitor certificate expiry dates; never let a certificate expire during a sprint

**Firewall:**
- Only necessary ports are open (80 for ACME challenge, 443 for HTTPS, 22 for SSH)
- Application service ports (e.g., 8000 for FastAPI) are NOT exposed directly to the internet — traffic goes through Nginx
- Changes to firewall rules are documented

**SSH Access:**
- You manage which team members have SSH access to the VPS
- SSH key-based authentication only — password authentication is disabled
- Onboard new team members by adding their public key to `authorized_keys`
- Off-board departing members by removing their key

**Reference:** See `vps/TransIP_VPS_Configuration.md` for Nginx configuration examples, SSL setup, firewall rules, and SSH configuration details.

### 3. Secrets & Security

**You are the guardian of credentials.** This responsibility is non-negotiable.

**Where secrets live:**
- All secrets (database passwords, API keys, JWT secrets, SSH keys) are stored in **GitHub repository secrets**
- Secrets are scoped to the correct environment (dev secrets are separate from prod secrets)
- You document which secrets exist and what they are for — but **NEVER document their values**

**Where secrets must NEVER live:**
- Source code files
- `.env` files committed to the repository
- GitHub Actions workflow files (as hardcoded values)
- Teams messages, Jira comments, or any chat platform
- Documentation

**Your responsibilities:**
- Audit secrets in all 4 repos at the start of the project (Sprint 0)
- If secrets are found in code: rotate them immediately and move to GitHub secrets
- When a developer adds a new environment variable, you add it to GitHub secrets for each environment
- Enable GitHub secret scanning where available
- Maintain a `.gitignore` that excludes `.env` files in all repos

### 4. Deployment & Release

**You make deployments predictable and safe.**

**Three environments:**
- `dev` — auto-deploys from the `dev` branch; used for ongoing integration
- `test` — manually triggered; used by Tester to verify completed stories
- `prod` — manually triggered after Sprint Review sign-off; the demo environment

**Deployment process:**
- Document the deployment process step by step in a runbook accessible to the whole team
- Any team member should be able to trigger a deployment without needing you present
- Every deployment is logged: story ID, time, who triggered it, which environment, any issues

**Coordination:**
- When a story is marked Done by the Tester, you deploy it to the test environment and confirm it's up
- 24 hours before Sprint Review, you deploy everything to the prod/demo environment and verify it
- You notify the team (via Teams) when deployments complete or when they fail

**Scripts:**
- Deployment steps are scripted, not done manually; the script lives in the repository
- Scripts are version-controlled alongside the pipeline files

### 5. Monitoring & Incident Response

**You detect problems before the team does.**

**Monitoring:**
- Set up basic uptime monitoring for each environment (even a simple cron job that pings the app and sends a Teams alert on failure)
- Check pipeline health at the start of each sprint: are all branches green?
- Monitor disk space, memory, and CPU on the VPS — resource exhaustion causes unexpected outages
- Review Nginx error logs periodically for signs of problems

**Incident response:**
- When an environment goes down, you respond within 30 minutes during sprint hours
- You have a runbook ready: "What to check first when the app is down"
- You notify the Scrum Master immediately if an outage impacts the team's ability to work
- After an incident: document what happened, what caused it, and how to prevent it

**Escalation path:**
- Minor pipeline failures → diagnose and fix yourself
- Environment outage → diagnose, fix, notify SM if not resolved in 30 minutes
- Security incident (credentials exposed) → notify staff immediately

### 6. Team Documentation & Enablement

**You make yourself replaceable — by documenting everything.**

**Runbook:**
- A runbook is a document that describes how to perform common operational tasks
- Your runbook covers: how to deploy, how to restart a service, how to renew SSL, how to add a new environment variable, what to check when the app is down
- The runbook is stored in a shared location (the repository or a Teams wiki)
- The runbook is written for the team — not just for yourself; anyone should be able to follow it

**Team enablement:**
- At the end of Sprint 0, walk the team through the deployment process — they should be able to trigger a deployment without you
- When you add a new pipeline step, explain it in the PR description: "What does this do and why?"
- When a developer asks about the pipeline, take 5 minutes to explain it — this reduces the "DevOps is a black box" problem
- Share your incident post-mortems in retrospectives so the whole team learns from infrastructure issues
