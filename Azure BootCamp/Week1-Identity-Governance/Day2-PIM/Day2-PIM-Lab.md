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
2. Explore eligible vs active assignments
3. Configure approval workflow for a role
4. Activate a role (e.g., User Administrator)
5. Create an Access Review
6. Review Access Review results

## Validation
- Role activation requires justification
- Approval workflow triggers (if configured)
- Access Review shows correct users

## Troubleshooting
- If PIM doesn’t show roles → ensure Azure AD Premium P2 trial is active
- If activation fails → check MFA requirement
- If Access Review doesn’t populate → check scope selection

## Governance Relevance
- PIM enforces just‑in‑time access
- Access Reviews ensure least privilege over time