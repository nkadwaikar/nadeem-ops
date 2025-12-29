# Day 2 — Privileged Identity Management (PIM) + Access Reviews

## Chapters to Read
- Chapter 1 (PIM section)
- Chapter 3 (Governance intro)

## Learning Objectives
- Understand PIM concepts
- Configure eligible vs active roles
- Create Access Reviews
- Understand governance workflows

## Lab Steps
1. Open Entra ID → Privileged Identity Management
2. Review eligible vs active role assignments
3. Configure approval workflow for a privileged role
4. Activate a role (e.g., User Administrator)
5. Create an Access Review for a group or role
6. Review Access Review results and document findings

## Validation
- Role activation requires justification and MFA (if configured)
- Approval workflow triggers correctly
- Access Review shows correct users and status
- Review results reflect expected compliance

## Troubleshooting
- If PIM roles don’t appear → ensure Azure AD Premium P2 trial is active
- If activation fails → verify MFA requirement and role eligibility
- If Access Review is empty → check scope (group vs role)
- If approval workflow doesn’t trigger → confirm approver assignment

## Governance Relevance
- PIM enforces just‑in‑time access
- Access Reviews maintain least privilege over time
- Approval workflows add governance and auditability