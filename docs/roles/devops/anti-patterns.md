# DevOps Engineer — Anti-Patterns (What Goes Wrong)

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
