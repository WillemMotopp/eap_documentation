# DevOps Engineer — Concrete Tasks

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
