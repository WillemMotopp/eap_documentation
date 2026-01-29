---
Document: Definition_of_Done_Template
Version: 1.2
Status: Draft
Audience: Interns
Approval required: Yes
Changes from v1.1: Added privacy & data protection checkpoint
---

# Definition of Done (Template)

Each team creates its own Definition of Done.  
Use this template as a starting point.

## Code
- Code is readable and reviewed by at least one team member
- No critical warnings or errors
- Code follows agreed coding standards

## Testing
- Unit tests are added or updated where relevant
- Tests pass in CI
- Test coverage is adequate for the changes made

## DevOps
- Build succeeds
- Relevant automated tests are executed as part of the pipeline
- Deployment works in the target environment (if applicable)

## Quality & Resilience
- The application behaves predictably under failure conditions
- Errors are logged clearly
- Recovery or rollback is possible

## Documentation
- Changes are documented
- Setup instructions are updated (if applicable)
- API documentation is updated (if applicable)

## Architecture
- Architectural impact is documented (if applicable)
- If significant architectural decisions were made:
  - Architecture Decision Record (ADR) is written
  - ADR is reviewed and accepted by the team
  - Architecture diagrams are updated (if needed)

## Privacy & Data Protection
- Personal data handling is reviewed (if applicable)
- No sensitive data exposed in logs or error messages
- Data retention implications are considered
- Access controls prevent unauthorized data access
- Privacy by design principles are followed

## Agreement
- The team agrees this work is "Done"
- Done means ready to show in a Sprint Demo and ready to be used by others

---

## Notes on "if applicable"

Not every item requires all these checkpoints:
- **Small bug fixes** may not need architecture documentation
- **UI-only changes** may not affect API documentation
- **Internal refactoring** may not need updated setup instructions

Use professional judgment as a team.  
When in doubt, document.

---

**End of Definition of Done Template v1.1**
