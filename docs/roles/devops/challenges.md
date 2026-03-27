# DevOps Engineer — Common Challenges & Solutions

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
