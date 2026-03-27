# DevOps Engineer — Quick Reference Checklists

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
