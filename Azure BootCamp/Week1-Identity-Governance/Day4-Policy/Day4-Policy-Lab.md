## Chapters to Read
- Chapter 3 — Manage Subscriptions & Governance

## Learning Objectives
- Understand governance hierarchy
- Deploy Management Groups
- Assign built‑in and custom policies
- Validate compliance

## Lab Steps
1. Create a Management Group
2. Move subscription under the Management Group
3. Assign a built‑in policy (e.g., require tags)
4. Create a simple custom policy (JSON)
5. Assign the custom policy
6. Validate compliance results

## Validation
- Subscription appears under the MG
- Built‑in policy shows compliance state
- Custom policy evaluates correctly
- Non‑compliant resources appear in the compliance tab

## Troubleshooting
- If MG creation fails → ensure Tenant Root permissions
- If policy doesn’t apply → check assignment scope
- If compliance doesn’t update → wait 5–10 minutes
- If custom policy errors → validate JSON structure

## Architecture Relevance
- MGs enforce enterprise‑wide governance
- Policies prevent misconfigurations
- Compliance ensures continuous enforcement