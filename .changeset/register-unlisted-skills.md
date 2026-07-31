---
"mattpocock-skills": patch
---

Ship the skills that were already in the repo but missing from the plugin. The **`implement`** skill (implement a piece of work from a PRD or set of issues, leaning on `/tdd` at pre-agreed seams) and the **`resolving-merge-conflicts`** skill (recover each side's intent, resolve every hunk, run the project's checks, finish the merge) are now registered in `plugin.json` and listed in the top-level and bucket READMEs. The four `misc` skills — **`git-guardrails-claude-code`**, **`migrate-to-shoehorn`**, **`scaffold-exercises`**, and **`setup-pre-commit`** — are now in `plugin.json` too, as the repo's registration rule requires, and the `misc` lists are grouped under **Model-invoked** to match the other buckets.
