# DevOps Engineer — Good Practice Scenarios

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
