# DevOps Engineer Role Guide

**Version:** 1.0
**Date:** 2026-03-26
**Audience:** Trainees (DevOps Engineer role)
**Purpose:** Clear expectations, responsibilities, and practical guidance

---
[TOC]
---

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

---

## Concrete Tasks

### During Sprint 0 (Preparation Week)

**Your ONLY job this week: Build the foundation the team needs to work.**

**Day 1:**
- [ ] SSH into the TransIP VPS and verify access works
- [ ] Read `vps/TransIP_VPS_Configuration.md` end-to-end (not skimming — read it carefully)
- [ ] Check the existing Nginx configuration: what virtual hosts exist? what is currently running?
- [ ] Check SSL certificate expiry date: `sudo certbot certificates`
- [ ] Verify GitHub Actions are enabled on all 4 repositories (eap-architecture, eap-backend, eap-frontend, eap-qa)
**Day 2:**
- [ ] Review existing pipeline files (`.github/workflows/`) in each of the 4 repos
- [ ] Document what each existing pipeline does: which events trigger it, what steps run, what environments it deploys to
- [ ] Identify any pipelines that are broken (failing) or missing entirely
- [ ] Note which pipelines are missing test steps — this becomes your Sprint 0 improvement list

**Day 2–3:**
- [ ] Set up three environments: `dev`, `test`, and `prod`
  - `dev`: auto-deploys from the `dev` branch on every merge
  - `test`: triggered manually for QA verification
  - `prod`: triggered manually after Sprint Review sign-off
- [ ] Configure Nginx virtual hosts for each environment (e.g., `dev.yourapp.example.com`, `test.yourapp.example.com`, `yourapp.example.com`)
- [ ] Issue SSL certificates for each environment domain via Certbot
- [ ] Verify each environment URL is accessible from outside the VPS (test in your browser)
- [ ] Post the environment URLs in the Teams channel: "Environment URLs: dev → [...], test → [...], prod → [...]"

**Day 3–4:**
- [ ] Audit secrets across all 4 repositories:
  - Search for `.env` files committed to git: `git log --all --full-history -- "**/.env"`
  - Search for hardcoded credentials in workflow files
  - Search for API keys or passwords in configuration files
- [ ] If any secrets are found in code: rotate them immediately and move to GitHub repository secrets
- [ ] Verify that all required secrets exist in GitHub repository secrets for each environment
- [ ] Document which secrets exist and what they are for (names only, not values) — store this in the runbook

**Day 4–5:**
- [ ] Write the "How to Deploy" runbook for the team:
  - Step-by-step guide to trigger a deployment for each environment
  - Where to find environment URLs
  - How to check deployment logs in GitHub Actions
  - Who to contact (and how) if a deployment fails
- [ ] Share the runbook with the team and ask them to read it
- [ ] Walk the team through the runbook in a 15-minute session: "Here's how deployment works"
- [ ] Set up Certbot auto-renewal via cron: `0 12 * * * /usr/bin/certbot renew --quiet`
- [ ] Set up basic uptime monitoring (even a simple ping script with Teams notification on failure)

**End of Sprint 0:**
- [ ] All pipelines run successfully (green) on all 4 repos
- [ ] Three environments exist and are accessible via HTTPS
- [ ] No secrets exist in code or committed `.env` files
- [ ] Secret names (not values) are documented
- [ ] Team has read and confirmed they can follow the deployment runbook
- [ ] Certbot auto-renewal is configured and tested
- [ ] Uptime monitoring is in place

**Success criteria:** Any team member can trigger a deployment to the test environment by following the runbook — without needing to ask you for help.

### During Each Sprint (Ongoing)

**Beginning of Sprint (Sprint Planning):**
- [ ] Check pipeline health on all 4 repos before Sprint Planning starts — are all branches green?
- [ ] Verify all environment URLs are accessible
- [ ] Review any pipeline failures from the previous sprint: were they resolved? are there recurring patterns?
- [ ] Attend Sprint Planning: listen for stories that have DevOps implications (new environment variables, new services, infrastructure changes)
- [ ] If a story requires infrastructure work (new secret, new service, environment change), flag it: "Story X will need a new environment variable added — I'll coordinate with the developer"

**Daily:**
- [ ] Check for pipeline failure notifications in GitHub or Teams
- [ ] If a pipeline breaks due to a code change: notify the developer in Teams and help diagnose
- [ ] A pipeline broken for more than 2 hours is a **team impediment** — report it in standup
- [ ] Respond to DevOps questions from team members within a few hours during sprint hours

**Per Story Deployment (when Tester marks story as Done):**
- [ ] Trigger deployment of the story's branch to the test environment
- [ ] Verify the application starts successfully — check the deployment logs
- [ ] Confirm the specific feature is accessible (do a basic smoke test)
- [ ] Notify Tester in Teams: "Story EAP-XXX is deployed to test at [URL]. Ready for testing."
- [ ] Log the deployment: story ID, time, environment, who triggered it, any issues

**Sprint Review Preparation (24 hours before Sprint Review):**
- [ ] Deploy all completed stories to the prod/demo environment
- [ ] Verify the demo environment URL is accessible from outside the VPS
- [ ] Test the main user flows manually: login, submit a request, check a dashboard — whatever will be shown
- [ ] Check that SSL is valid: no browser security warnings on any environment
- [ ] Notify SM: "Demo environment is ready at [URL]. I've verified [specific flows] work."

**End of Sprint (Retrospective):**
- [ ] Write a brief sprint pipeline report: number of pipelines run, failures, deployments made, any incidents
- [ ] Share the report in retrospective or the Teams channel
- [ ] Identify one pipeline improvement to implement next sprint (e.g., adding a new test step, improving deployment speed)
- [ ] Update the runbook if anything changed during the sprint

---

## Good Practice Scenarios

### Scenario 1: Setting Up a New Pipeline Step

**Context:** Sprint 2. Developers have been writing pytest tests for the FastAPI backend, but the tests aren't running automatically in CI. The Scrum Master raises it in standup: "We wrote all these tests, but they aren't automated in the pipeline. Can we fix that?"

**What DevOps does:**

Before acting, DevOps reviews the existing pipeline file:

> **DevOps (in standup):** "I'll look at the backend pipeline today and add a pytest step. Developer A, can you confirm which test command you're using — is it `pytest tests/` or something else?"

**Developer A:** "It's `pytest --cov=app tests/` — we're using coverage reporting too."

**DevOps:** "Perfect, I'll wire that in."

DevOps opens the existing `.github/workflows/backend.yml`, finds the job that runs on pull requests, and adds the test step after the dependency installation step:

```yaml
- name: Run tests with coverage
  run: pytest --cov=app tests/
  env:
    DATABASE_URL: ${{ secrets.TEST_DATABASE_URL }}
```

DevOps opens a pull request with the change. In the PR description:

> "Added pytest step to the backend CI pipeline. Tests now run automatically on every PR. Coverage report will appear in the CI output.
>
> **Note to Developer A:** Can you check the test output in the CI run and confirm it looks right? I want to make sure the env vars are wired correctly before we merge."

Developer A checks, confirms the output looks correct, and approves.

After merge:
- Every PR to the backend repo now runs tests automatically
- Coverage report is visible in the CI output without manual intervention

DevOps updates the runbook: "Backend tests run automatically on every PR. If tests fail, the PR cannot be merged until the developer fixes them."

In the next standup:

> **DevOps:** "Pipeline update is in. Backend tests now run on every PR. If your PR fails CI because of a test, that's a feature, not a bug — please fix the test before merging."

**Why this is good:**
- The change was introduced via a pull request, not a direct commit to main — the change is reviewable and reversible
- DevOps involved the developer to verify the output rather than guessing
- The runbook was updated so the team knows what to expect
- The standup message set clear expectations about what failing tests mean

---

### Scenario 2: Diagnosing and Resolving a Broken Deployment Mid-Sprint

**Context:** Sprint Day 5. Developer B merges a PR that introduces a database migration requiring a new environment variable. The deployment pipeline runs automatically, fails, and the application on the test environment goes down. Tester can't test anything. An alert appears in the Teams DevOps channel.

**What DevOps does:**

DevOps sees the failure notification within 15 minutes and immediately opens the GitHub Actions run log.

The last lines of the log read:

```
ERROR: Environment variable DATABASE_MIGRATION_URL is not set.
Application failed to start.
```

DevOps identifies the root cause: the new migration introduced a new required environment variable that isn't in GitHub secrets for the test environment.

DevOps posts in Teams immediately:

> **DevOps:** "Test environment is down — I can see the pipeline failed because a new environment variable `DATABASE_MIGRATION_URL` is missing from our test secrets. Developer B, what value should this be for the test environment? I'll add it to GitHub secrets as soon as you share it. (Please share it via a private message, not in this channel.)"

**Developer B (DM to DevOps):** "It should be [value]. Same as DATABASE_URL but pointing to the migrations schema."

DevOps adds the secret to GitHub repository secrets for the test environment, then re-triggers the deployment pipeline manually.

DevOps posts in Teams:

> **DevOps:** "Secret added. Re-triggering deployment now."

Three minutes later:

> **DevOps:** "Test environment is back up. Tester, you should be able to access [URL] again. Total downtime: 28 minutes."

DevOps then updates the runbook:

> "**When adding a new environment variable:** Before merging the PR that introduces it, notify DevOps with the variable name and value for each environment. DevOps will add it to GitHub repository secrets so the deployment doesn't fail."

DevOps raises it in the next standup:

> **DevOps:** "We had a 28-minute outage on test yesterday because a new env var wasn't in secrets before the deployment ran. No blame — this is a process gap. Going forward, if your code needs a new env var, DM me before merging so I can add it to secrets first. I've added this to the runbook."

**Why this is good:**
- Response was fast (28 minutes total downtime — well within the 30-minute target)
- Root cause was identified immediately from the logs (not just "the build failed")
- DevOps did not blame the developer; the framing was "process gap," not "Developer B's fault"
- The credentials were shared via private message, not a public Teams channel
- The runbook was updated with a prevention step
- The standup message was informational and constructive

---

### Scenario 3: Hardening Secrets Management After a Near-Miss

**Context:** Sprint 3. DevOps is reviewing a PR from Developer C. The changed files include application code, but Developer C also accidentally staged a `.env` file. The `.env` file is in `.gitignore` and was not committed — it appears in the PR diff as an untracked change that was staged but not included in the commit. DevOps notices the warning GitHub shows: "Some changes were staged but not committed."

**What DevOps does:**

DevOps does not just close the review and move on.

DevOps comments on the PR:

> **DevOps (PR comment):** "Hey, I noticed a `.env` file was staged in your local working tree when you made this commit. It didn't make it into the commit because it's in `.gitignore` — so you're fine this time. But I want to make sure we talk about this as a team so it doesn't happen to anyone else. I'll raise it in standup. The PR itself looks good — approving."

In standup, DevOps takes 5 minutes:

> **DevOps:** "Quick heads-up about secrets. Developer C nearly committed a `.env` file yesterday — it was caught by `.gitignore`, so no credentials were exposed. But I want to show why this matters and what we can do about it."

DevOps shares screen and shows the team:

1. Where `.gitignore` is and why `.env` is excluded
2. What would have happened if `.env` *had* been committed: the credentials would be in git history permanently, visible to anyone with repo access, and would need to be rotated immediately
3. How to check what's staged before committing: `git status` and `git diff --staged`

DevOps then adds a git pre-commit hook to all repos that checks for common secret patterns and prevents accidental commits. DevOps also enables GitHub's built-in secret scanning on all 4 repositories.

DevOps updates the team's onboarding checklist:

> "Before your first commit: run `git status` and verify no `.env` files are staged. Never commit credentials — not even temporarily."

DevOps adds a note to the runbook:

> "Secret scanning is enabled on all repositories. If GitHub detects a credential pattern in a commit, it will alert the repository owner. If you receive such an alert: notify DevOps immediately and assume the credential is compromised."

**Why this is good:**
- A near-miss was turned into a team learning moment rather than quietly ignored
- DevOps did not embarrass Developer C — the issue was raised constructively and framed as a team topic
- Two layers of systematic protection were added (pre-commit hook + GitHub secret scanning) — not just a verbal warning
- The team now understands *why* secrets in code are dangerous, not just that they're forbidden
- The runbook was updated so the response procedure is clear if scanning triggers an alert in the future

---

## Anti-Patterns (What Goes Wrong)

### Anti-Pattern 1: "It Deploys Manually"

**What it looks like:**

Every deployment happens like this:

> **Developer:** "Can you deploy the latest version to test?"
>
> **DevOps:** "Sure, give me a few minutes."
>
> [DevOps SSHs into the VPS, runs `git pull && docker-compose restart`, checks it works]
>
> **DevOps:** "It's up."

No pipeline file exists. No GitHub Actions runs are visible. The team has no idea what was deployed, when, or whether the tests passed before deployment.

When DevOps is sick or absent:

> **Developer:** "We need to deploy for the Sprint Review tomorrow."
>
> **Scrum Master:** "DevOps is out. Does anyone else know how to deploy?"
>
> **Team:** "...No."

**Why it's bad:**
- **Single point of failure:** If DevOps is absent, nothing deploys — the team is completely blocked
- **No audit trail:** Nobody knows what was deployed, when, or whether tests passed
- **Deployment errors aren't caught:** Automated tests that could catch issues before deployment never run
- **Team is blocked waiting for DevOps:** Tester can't test, Sprint Review is at risk
- **Not scalable:** As the sprint progresses and more stories are done, the manual process becomes a daily bottleneck

**Symptoms:**
- Team asks DevOps "Can you deploy this for me?" instead of triggering it themselves
- Sprint Review preparation is last-minute and stressful
- There are no `.github/workflows/` pipeline files, or they exist but don't deploy anything
- "DevOps is busy" appears as a reason for delayed testing

**How to fix it:**

Write a GitHub Actions deployment workflow — even a simple one:

```yaml
name: Deploy to Test
on:
  workflow_dispatch:
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy via SSH
        run: |
          ssh ${{ secrets.VPS_USER }}@${{ secrets.VPS_HOST }} \
            'cd /app && git pull && systemctl restart app'
```

Document it so any team member can trigger it from the GitHub Actions UI.

Never deploy manually again. If you're tempted to SSH in and run commands manually: stop, write a script or pipeline step first, then run it via the pipeline.

**The rule: "If I've done it manually twice, I write a script."**

---

### Anti-Pattern 2: Secrets in Code

**What it looks like:**

During Sprint 1, a developer commits a `.env` file with real credentials to the `dev` branch. In Sprint 2, a shortcut is taken in a GitHub Actions workflow file:

```yaml
env:
  API_KEY: abc123xyz-real-key-here
  DB_PASSWORD: realpassword123
```

Both are now in git history — permanently. Even if the files are deleted later, the credentials remain accessible to anyone who can read the repository's git history.

**Why it's bad:**
- **Credentials are exposed in git history forever** — deleting the file does not remove it from history
- **Any contributor, past or present, can read the credentials** — this is a security breach
- **All exposed credentials must be rotated immediately** — the rotation process takes time and can break running environments
- **If the repository is ever made public** (e.g., for a portfolio), the credentials become public
- **A compromised database password can expose personal data** — this is a GDPR incident, not just a technical problem

**Symptoms:**
- `.env` files appear in `git log --all -- "**/.env"`
- API keys or passwords appear in workflow files (`.github/workflows/*.yml`)
- Credentials are shared in Teams messages or Jira comments
- README or documentation contains example credentials that are real

**How to fix it:**

**Immediately, upon discovery:**
1. Rotate ALL exposed credentials — assume they are compromised, even if you think nobody saw them
2. Remove the credential from git history using `git filter-branch` or BFG Repo Cleaner (ask staff for help if needed)
3. Add the credential to GitHub repository secrets
4. Verify `.env` is in `.gitignore` — if not, add it

**Prevention:**
- Enable GitHub secret scanning on all repositories (Settings → Security)
- Add a pre-commit hook that warns when credential patterns are detected
- Add to team onboarding: "Never commit `.env` files. Never hardcode credentials."
- In PR reviews: always check workflow files for hardcoded values

**After the incident:**
- In the next retrospective: "A credential was exposed. Here's what happened, what we did, and how we prevent it."
- If personal data may have been accessible due to the exposed credential: notify staff — this may be a GDPR incident requiring formal reporting

---

### Anti-Pattern 3: "Deploy and Forget" DevOps

**What it looks like:**

DevOps works extremely hard in Sprint 0: sets up all the pipelines, configures Nginx and SSL, writes a runbook, deploys the initial application. By the end of Sprint 0, everything is working perfectly.

Sprint 1 begins. DevOps considers the infrastructure work complete and focuses on other things. No monitoring is set up. The runbook hasn't been updated in two sprints.

**Sprint 3, Day 6:**

> **Tester:** "The test environment has been down since this morning. I've been trying to test Story EAP-47 all day."
>
> **DevOps:** "What? When did it go down?"
>
> **Tester:** "I don't know — I noticed it at 9am."
>
> **DevOps:** "I didn't get any notification... let me check."

Diagnosis takes 45 minutes because nobody has looked at the VPS since Sprint 1. The disk is full. The application crashed when it ran out of space to write logs. There is no runbook entry for "disk full."

Total outage: 6 hours. Sprint Review is tomorrow.

**Why it's bad:**
- **Downtime goes undetected** — nobody found out for hours because there was no monitoring
- **No recovery procedure** — diagnosing the issue took much longer than it should have
- **Team is paralyzed** — Tester loses a full day; QA stories can't be verified
- **Sprint Review is at risk** — the environment may not be stable in time
- **DevOps is surprised** — which means the team loses confidence in the infrastructure

**Symptoms:**
- Team discovers outages from Tester complaints rather than from monitoring
- There is no runbook entry for common failure modes
- Incident duration is long because nobody knows the recovery steps
- DevOps hasn't looked at the VPS since Sprint 0
- DevOps says "I already set it up" when asked about monitoring

**How to fix it:**

**Set up basic monitoring — even something simple:**
```bash
# Cron job: every 5 minutes, ping the app; send Teams webhook if it fails
*/5 * * * * curl -sf https://yourapp.example.com/health || \
  curl -X POST $TEAMS_WEBHOOK -d '{"text":"⚠️ App is unreachable!"}'
```

**Write a "What to check when the app is down" runbook entry:**
1. Check Nginx: `sudo systemctl status nginx`
2. Check the application service: `sudo systemctl status app-name`
3. Check disk space: `df -h`
4. Check memory: `free -h`
5. Check recent deployment logs: open GitHub Actions, look at the last deployment run
6. Check Nginx error log: `sudo tail -100 /var/log/nginx/error.log`

**Define an SLA for incident response:**
"If the application is down during sprint hours (9:00–17:00), DevOps responds within 30 minutes."

**Run a fire drill (optional but recommended):**
Simulate an outage. Stop the application service on the VPS. Time how long it takes to detect, diagnose, and resolve. Use the result to improve your runbook.

---

### Anti-Pattern 4: Overengineered Pipeline

**What it looks like:**

**Sprint 0:** DevOps researches modern DevOps tooling and decides to build the "right" infrastructure from the start. Plans include:
- Kubernetes cluster on the TransIP VPS
- Helm charts for each service
- Terraform for infrastructure-as-code
- Prometheus and Grafana for monitoring
- ArgoCD for GitOps-based deployments
- Vault for secrets management

By the end of Sprint 2, the Kubernetes cluster is configured but unstable. The backend hasn't been deployed yet because the Helm chart needs more work. Developers can't run the application locally because the Docker setup changed. DevOps is the only person who understands any of it.

**Sprint 3 standup:**

> **Developer A:** "I can't run the backend locally — the new Docker setup doesn't work."
>
> **Developer B:** "Me neither. We need DevOps to help us every time we want to run the app."
>
> **Tester:** "I still can't access the test environment."
>
> **DevOps:** "The Helm chart needs one more fix and it'll all be working — probably by end of week."

**Why it's bad:**
- **Complexity the team can't maintain** — when the DevOps trainee leaves, nobody can manage the infrastructure
- **DevOps is the bottleneck for everything** — developers need DevOps to fix their local setup, Tester needs DevOps to access test environment
- **Wasted sprint time** — 2+ sprints spent on tooling instead of delivering product value
- **Product Owner and Scrum Master have no visibility** — nothing deployed means nothing to review
- **Knowledge leaves with the trainee** — the next cohort inherits infrastructure nobody understands

**Symptoms:**
- Team can't deploy without DevOps present
- Infrastructure changes take a full sprint to complete
- Team members don't understand how the pipeline works
- Complex tools are being used to solve simple problems
- "We're setting up infrastructure" appears as a reason for not having a working application to demo

**How to fix it:**

**Start with the simplest thing that works:**
- A `Dockerfile` that builds the application
- A `docker-compose.yml` for local development
- A GitHub Actions workflow that builds, tests, and deploys via SSH
- That's it. This is enough for a 10-week training program with 5 users.

**Ask before adding complexity:**
- "Will another trainee be able to maintain this without me?"
- "Does the team understand what this does?"
- "Are we using this tool because we need it, or because it's interesting?"
- "Does this complexity solve a problem we actually have right now?"

**Introduce complexity only when the current setup is genuinely insufficient:**
- Add Kubernetes when you have auto-scaling requirements (you won't)
- Add Terraform when you have multiple environments across cloud providers (you won't)
- Add Prometheus when you need custom metrics dashboards (a cron job ping is enough)

**The rule: Simple and working beats complex and fragile.**

---

## Common Challenges & Solutions

### Challenge 1: "A pipeline is broken and I don't know why"

**The situation:** A pipeline fails with a long, confusing log. The error message isn't immediately obvious. You've read through the log twice and can't identify the problem.

**Solution — step by step:**

**Step 1: Read from the bottom up.**
GitHub Actions logs show the most recent output at the bottom. The root cause error is almost always in the last 20–50 lines of the log. Errors earlier in the log are often just consequences of the root cause.

**Step 2: Identify what type of failure it is.**
- **Missing environment variable:** `Error: Environment variable X is not set` → add the secret to GitHub repository secrets
- **Dependency installation failure:** `Package not found` or `pip install failed` → version mismatch or network issue; check the package name and version
- **Test failure:** `FAILED tests/test_X.py::test_Y` → the code has a bug; contact the developer who last changed that code
- **SSH/deployment failure:** `Permission denied (publickey)` → the SSH key isn't set up correctly for the target environment
- **Docker build failure:** `COPY failed: file not found` → the Dockerfile references a file path that doesn't exist

**Step 3: Google the exact error message.**
Copy the error line from the log and search for it. GitHub Actions errors are common and well-documented. You will almost always find the solution within the first three search results.

**Step 4: Ask the developer who last changed the relevant code.**
> "The backend pipeline broke after your merge. The error is [paste error]. Do you know what might have caused this?"

The developer who introduced the change often knows immediately what's wrong.

**Step 5: If you've spent 1 hour and can't fix it, ask staff.**
An unresolved pipeline is a team impediment. Spending 3 hours debugging alone is less useful than getting unstuck in 5 minutes with staff guidance.

---

### Challenge 2: "SSL certificate expires soon"

**The situation:** You check the certificate expiry date and notice Certbot's automated renewal hasn't run (or you see a warning from your monitoring that the certificate expires in 14 days).

**Solution:**

**Step 1: Run renewal manually.**
```bash
sudo certbot renew
```

**Step 2: Check the output.**
- If renewal succeeds: `Congratulations, all renewals succeeded.`
- If renewal fails: read the error message

**Common failure reason — port 80 not open:**
Certbot uses the ACME HTTP-01 challenge, which requires port 80 to be accessible. If your firewall is blocking port 80, renewal will fail.

```bash
# Check if port 80 is open
sudo ufw status
# If port 80 is not listed as ALLOW, add it temporarily for renewal:
sudo ufw allow 80
sudo certbot renew
# After renewal succeeds, you can restrict port 80 again if needed
# (but Nginx needs it open for HTTP-to-HTTPS redirects anyway)
```

**Step 3: After renewal, restart Nginx.**
```bash
sudo systemctl restart nginx
```

**Step 4: Verify the certificate is now valid.**
```bash
sudo certbot certificates
```
Check the expiry date — it should now be 90 days from today.

**Step 5: Verify automated renewal is configured.**
```bash
# Check cron jobs
crontab -l
# Should include a line like:
# 0 12 * * * /usr/bin/certbot renew --quiet
```

If automated renewal isn't set up:
```bash
crontab -e
# Add:
0 12 * * * /usr/bin/certbot renew --quiet
```

**Step 6: Update the runbook with the renewal procedure.**

Reference: `vps/TransIP_VPS_Configuration.md` contains the full SSL configuration details.

---

### Challenge 3: "A developer needs a new environment variable"

**The situation:** Developer A is working on a story that integrates with a third-party API. The integration requires an API key. Developer A sends you a message: "I need to add an API_KEY environment variable. How do I do that?"

**Solution:**

**What you do NOT do:**
- Tell the developer to add it to a `.env` file and commit it
- Tell the developer to hardcode it in the application code temporarily
- Put the value in a Teams message or Jira comment

**What you do:**

**Step 1: Gather the information.**
Reply to the developer:
> "Got it. Can you tell me:
> 1. What's the exact variable name? (e.g., `EXTERNAL_API_KEY`)
> 2. Which environments need this? (dev, test, prod, or all three?)
> 3. Can you send me the value(s) via private message — not in this channel."

**Step 2: Add the secret to GitHub repository secrets.**
- Go to the repository on GitHub → Settings → Secrets and variables → Actions
- Click "New repository secret"
- Name: `EXTERNAL_API_KEY`
- Value: [the value the developer sent via DM]
- Repeat for each environment repository (or each environment's secret set)

**Step 3: Ensure the secret is referenced in the pipeline.**
Check the relevant GitHub Actions workflow file. If it doesn't pass the secret to the deployment step, add it:

```yaml
env:
  EXTERNAL_API_KEY: ${{ secrets.EXTERNAL_API_KEY }}
```

**Step 4: Update the secret documentation.**
Add the variable name (not its value) to the list of secrets in the runbook: "What secrets exist and what are they for."

**Step 5: Notify the developer.**
> "EXTERNAL_API_KEY has been added to GitHub secrets for [environments]. Re-trigger the deployment and it should be available. Let me know if the app can't read it."

**Step 6: Re-trigger the deployment.**
Secrets are only available to new pipeline runs — you need to re-trigger the deployment pipeline for the change to take effect.

---

### Challenge 4: "The application is down during Sprint Review"

**The situation:** It's 5 minutes before Sprint Review. You open the demo environment URL in your browser and get a connection error. The application is unreachable.

**Solution:**

**This is why you do the Sprint Review preparation checklist 24 hours in advance.** If you followed the checklist, you caught this yesterday and fixed it with time to spare.

If it happens anyway, despite preparation:

**Step 1: Do not panic. You have a runbook.**

**Step 2: Check the most common causes in this order (each check takes under 1 minute):**

```bash
# Is Nginx running?
sudo systemctl status nginx

# Is the application service running?
sudo systemctl status your-app-name

# Is disk space full?
df -h

# Is memory exhausted?
free -h
```

**Step 3: Apply the fix for the most common causes:**

- **Nginx stopped:** `sudo systemctl start nginx`
- **Application service stopped:** `sudo systemctl start your-app-name`
- **Disk full:** Check what's taking space (`du -sh /var/log/*`), delete old logs if safe, then restart the service
- **Memory exhausted:** Restart the application service to free memory

**Step 4: If you can't fix it in 5 minutes, tell the Scrum Master immediately.**

> "The demo environment is down. I'm diagnosing. I may not be able to fix it before the review starts."

The Scrum Master can adapt — reschedule the demo segment, use a recording, or describe features verbally. They need to know immediately so they can make the call.

**Step 5: After Sprint Review, do a post-mortem.**

Document what happened:
- What time did the outage start? (Was it before or after your 24-hour check?)
- What was the root cause?
- How long did it take to diagnose and resolve?
- What can be added to the runbook or monitoring to prevent/detect this faster?

---

## Quick Reference Checklists

### Sprint 0 Checklist

- [ ] SSH into VPS — verify access works with your key
- [ ] Read `vps/TransIP_VPS_Configuration.md` end-to-end
- [ ] Check SSL certificate expiry date: `sudo certbot certificates`
- [ ] Review existing Nginx configuration: what virtual hosts exist?
- [ ] Review pipeline files in all 4 repos (`.github/workflows/`)
- [ ] Document what each existing pipeline does
- [ ] Identify broken or missing pipelines
- [ ] Set up `dev`, `test`, and `prod` environments on the VPS
- [ ] Configure Nginx virtual hosts for each environment
- [ ] Issue SSL certificates for each environment via Certbot
- [ ] Verify all environment URLs accessible via HTTPS
- [ ] Post environment URLs in Teams channel
- [ ] Audit secrets: no secrets in code or committed `.env` files
- [ ] Move any discovered secrets to GitHub repository secrets
- [ ] Rotate any secrets that were exposed in code
- [ ] Document which secrets exist (names only, not values)
- [ ] Write "How to Deploy" runbook and share with team
- [ ] Walk the team through the runbook (15-minute session)
- [ ] Set up Certbot auto-renewal: `0 12 * * * /usr/bin/certbot renew --quiet`
- [ ] Set up basic uptime monitoring with Teams notification on failure
- [ ] Verify all pipeline runs are green on all 4 repos

---

### Sprint Deployment Checklist (per story)

- [ ] Story is marked Done by the Tester
- [ ] CI pipeline passed on the story's branch
- [ ] Trigger deployment to test environment (via GitHub Actions, not manual SSH)
- [ ] Wait for deployment pipeline to complete — check the logs
- [ ] Verify the application starts successfully (no crash on startup)
- [ ] Do a basic smoke test: can you access the feature the story describes?
- [ ] Log the deployment: story ID, time, environment, who triggered it, any issues
- [ ] Notify Tester in Teams: "EAP-XXX is deployed to test at [URL]"

---

### Sprint Review Preparation Checklist

- [ ] **24 hours before:** Deploy all completed stories to the prod/demo environment
- [ ] Verify the deployment pipeline completed successfully (no errors in logs)
- [ ] Verify the demo environment URL is accessible from outside the VPS
- [ ] Open the URL in a browser tab you haven't used before (no cached session)
- [ ] Check for SSL errors: the browser should show a padlock, no security warnings
- [ ] Test the main user flows that will be demonstrated in Sprint Review
- [ ] Check disk space on the VPS: `df -h` — ensure there's headroom
- [ ] Notify SM: "Demo environment is ready at [URL]. I verified [specific flows] work."
- [ ] Keep the VPS terminal open during Sprint Review in case you need to react quickly

---

### Security & Access Checklist (new team member onboarding)

- [ ] Receive team member's SSH public key (via Teams or email — never by them committing it to a repo)
- [ ] Add public key to VPS `authorized_keys`: `echo "ssh-rsa [key]" >> ~/.ssh/authorized_keys`
- [ ] Verify team member can SSH into VPS with their key before declaring it done
- [ ] Add team member to the GitHub organization and grant access to all 4 repositories
- [ ] Verify team member can access Jira project
- [ ] Share environment URLs with team member (Teams channel or runbook — not via DM each time)
- [ ] Brief team member on secrets policy: "Never commit `.env` files. Never share credentials in Teams or Jira. All secrets go in GitHub repository secrets — ask me to add them."
- [ ] Do NOT share secret values with the team member — they access the application, not the secrets directly

---

### Incident Response Checklist

When the application is unreachable or behaving unexpectedly:

- [ ] Check Nginx status: `sudo systemctl status nginx`
- [ ] Check application service status: `sudo systemctl status [app-name]`
- [ ] Check disk space: `df -h`
- [ ] Check memory usage: `free -h`
- [ ] Check Nginx error log: `sudo tail -50 /var/log/nginx/error.log`
- [ ] Check recent deployment logs in GitHub Actions — was there a recent failed deployment?
- [ ] Check application logs: `sudo journalctl -u [app-name] -n 100`
- [ ] Apply fix based on root cause (see Common Challenges section)
- [ ] Verify application is accessible after fix
- [ ] Notify team in Teams: "App is back up. Outage was [duration]. Root cause: [brief explanation]."
- [ ] If outage is not resolved within 30 minutes during sprint hours: notify SM and staff
- [ ] After resolution: write a brief post-mortem and update the runbook

---

### Pipeline Health Check Checklist (start of each sprint)

- [ ] Open GitHub Actions for eap-architecture — are all recent runs green?
- [ ] Open GitHub Actions for eap-backend — are all recent runs green?
- [ ] Open GitHub Actions for eap-frontend — are all recent runs green?
- [ ] Open GitHub Actions for eap-qa — are all recent runs green?
- [ ] If any pipeline is red: identify the failing step and log it as an impediment
- [ ] Verify `dev` environment is accessible via HTTPS
- [ ] Verify `test` environment is accessible via HTTPS
- [ ] Check SSL certificate expiry: `sudo certbot certificates` (if within 30 days of expiry, renew now)

---

## Tips for Success

### 1. Automate Everything

**If you did it manually twice, write a script.**

This is the single most important DevOps principle. Manual steps are error-prone, undocumented, and create single points of failure. Every time you find yourself SSHing into the VPS to run commands, ask: "Could this be a pipeline step or a script?"

- Deployments are automated (GitHub Actions workflow)
- SSL renewal is automated (cron job)
- Uptime checks are automated (monitoring script)
- Manual steps are an exception, not the norm

### 2. Document as You Go

**Your runbook is the team's lifeline when you're not available.**

Write the runbook entry immediately after you do something, not at the end of the sprint. When you're in the middle of doing something, you know exactly what the steps are — write them down then, before you forget.

The test: "Could another team member follow this runbook and perform this task without calling me?" If not, the runbook is incomplete.

### 3. Monitor Proactively

**Find out about outages before the team does.**

The worst way to discover an outage is from a frustrated Tester in standup. Set up monitoring so you get the alert first, have already started diagnosing, and can report in standup: "We had an outage from 9:15 to 9:47 — it's resolved. Root cause was X."

This is the difference between being reactive (bad) and proactive (good).

### 4. Secrets Never Go in Code — Not Even Temporarily

**There is no such thing as a "temporary" credential in git.**

Once a secret is in git history, it's there forever — even after deletion. The word "temporary" does not apply to things committed to version control. Before committing anything, ask: "Does this file contain credentials?" If yes, do not commit it.

### 5. Keep It Simple

**The simplest pipeline the team can understand and maintain.**

Complexity has a cost. Every tool you add is something another team member has to understand, something that can break, and something the next cohort inherits. A simple deployment script that everyone understands is more valuable than a sophisticated GitOps pipeline that only you can manage.

### 6. Test Your Deployments

**Always verify the application works after deploying.**

A deployment pipeline that says "Success" but deploys a broken application is worse than no pipeline at all — because it gives false confidence. After every deployment:
- Open the application URL in a browser
- Verify the main functionality works
- Check the application logs for errors

### 7. Ask "Can Someone Else Maintain This?"

**If no, simplify.**

Before adding a new tool, configuration, or pipeline step, ask this question. If the answer is "no" or "probably not without significant explanation," you are adding complexity the team can't afford. Document it, simplify it, or reconsider whether you need it.

---

## Getting Help

### When to Ask Staff

- **Security incidents:** If credentials were exposed in code, in a Teams message, or anywhere outside of GitHub secrets — notify staff immediately, even if you think you've contained it
- **Infrastructure decisions beyond your access level:** If the VPS needs a configuration change that requires root-level access you don't have, or if you're considering a change that could take down the server
- **VPS configuration issues you can't resolve:** If you've been debugging for more than an hour and the application still isn't running, ask staff rather than spending another hour guessing
- **GDPR implications of infrastructure decisions:** If a new logging setup or monitoring tool would capture personal data, discuss with staff before implementing

### When to Ask Developers

- **What environment variables a new feature needs:** The developer who wrote the code knows which variables it requires — ask them before they merge, not after the deployment fails
- **Why a test is failing:** Application tests test application code; if a test fails, the developer who wrote the code should diagnose it — your job is to make sure the test runs in CI, not to fix the application logic
- **Deployment configuration they introduced:** If a developer added a new service or changed a port, they should explain it so you can update the pipeline accordingly
- **What a feature does:** Before Sprint Review, ask developers to briefly explain what each story does so you can verify it works after deploying

### When to Ask the Scrum Master

- **If a pipeline issue becomes a team impediment you can't resolve quickly:** A broken pipeline that blocks testing or deployment for more than 2 hours is an impediment — tell the SM so it can be tracked and escalated if needed
- **If a sprint is at risk due to infrastructure instability:** The SM needs visibility to manage expectations and re-plan if necessary
- **If a team member is not following secrets policy:** After you've addressed it with the person directly, if it continues, involve the SM
- **Process questions:** "Should I attend all Sprint ceremonies?" or "How should I report pipeline status in standup?" — the SM can advise

### When to Check the VPS Documentation

`vps/TransIP_VPS_Configuration.md` contains:
- Nginx configuration examples and virtual host setup
- SSL certificate management with Certbot
- Firewall rules and port configuration
- SSH setup and key management
- Service management commands

Check this document before asking staff for VPS-related questions — the answer is likely already there.

---

## Remember

**You are learning.** Nobody expects a perfect CI/CD setup with zero incidents in Sprint 1.

**Good DevOps Engineers:**
- Automate deployments so the team is never blocked waiting for you
- Document everything — the runbook is your most important deliverable
- Respond to incidents quickly and communicate clearly during outages
- Keep secrets secret — zero tolerance for credentials in code
- Keep the pipeline green — a broken pipeline is a broken team

**You don't need to:**
- Build complex infrastructure — simple and working beats complex and fragile; a Dockerfile and a GitHub Actions workflow are enough
- Know all DevOps tools — learn what the team actually needs, not what's trending
- Work alone — involve developers in pipeline design; they know what the code needs
- Fix every incident yourself — escalate to staff when you've been stuck for more than an hour

**Your success = Team can deploy reliably at any time, incidents are detected and resolved quickly, no credentials are ever exposed.**

---

**Questions?** Ask your Scrum Master, developers, or staff coach. For VPS-specific questions, refer to `vps/TransIP_VPS_Configuration.md`.

**END OF DEVOPS ENGINEER ROLE GUIDE**
