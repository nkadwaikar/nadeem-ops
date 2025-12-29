# Day 4 — Azure Policy + Management Groups

## Chapters to Read
- Chapter 3 — Manage Subscriptions & Governance

## Learning Objectives
- Understand governance hierarchy
- Deploy Management Groups
- Assign built‑in and custom policies
- Validate compliance

## Lab Steps
1. Create Management Group
2. Move subscription under the MG
3. Assign built‑in policy (e.g., require tags)
4. Create simple custom policy (JSON)
5. Assign custom policy
6. Validate compliance results

## Validation
- Subscription appears under MG
- Policy assignment shows “Compliant / Non‑compliant”
- Custom policy evaluates correctly

## Troubleshooting
- If MG creation fails → ensure permissions at tenant root
- If policy doesn’t apply → check assignment scope
- If compliance doesn’t update → wait 5–10 minutes

## Architecture Relevance
- MGs enforce enterprise‑wide governance
- Policies prevent misconfigurations
- Compliance ensures continuous enforcement