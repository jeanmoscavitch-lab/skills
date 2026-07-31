---
"mattpocock-skills": patch
---

Fix the **`implement`** skill's final step, which delegated to `/review` — a skill that lives in `in-progress/` and does not ship with the plugin, so the step dangled for every installed user. The step now states the review itself (check the work against the originating PRD or issues, and against the repo's coding standards) and treats `/review` as an optional accelerator rather than a hard dependency.
