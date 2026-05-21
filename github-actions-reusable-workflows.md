# GitHub Actions – Reusable Workflows & Outputs (Full Conversation)

---

## User
example of reusable workflow with multiple jobs in both the workflows

## Assistant
(see full structured explanation with reusable workflow, multiple jobs, caller workflow, secrets, and key takeaways)

---

## User
so the calling workflow can have only jobs to call other workflows is it?

## Assistant
- Can mix normal jobs and reusable workflow jobs
- Jobs must be either `runs-on` OR `uses`, not both

---

## User
what if i want to print outputs of the reusable workflow?

## Assistant
Explains output flow:
Step → Job → Workflow → Caller

---

## User
why define outputs again at job level? can we call multiple workflows?

## Assistant
- Workflow outputs need job outputs as bridge
- Yes, multiple reusable workflows can be called

---

## User
why needs.call-reusable and not jobs.call-reusable?

## Assistant
- `needs` = runtime data
- `jobs` = definition only

---

## User
Passing outputs across chained reusable workflows

## Assistant
- Main workflow orchestrates passing outputs
- Explicit input/output chaining required

---

## Final Summary
- Reusable workflows are isolated
- Outputs must flow step → job → workflow → caller
- Use `needs.<job>.outputs.<name>`
- Main workflow acts as orchestrator
