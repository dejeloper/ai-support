Review the changes between origin/main and the current local branch using `git diff origin/main...HEAD`. Do not create the PR, only generate the text.

Generate the following in English:

**Title:**
type: Short descriptive title following conventional commits (feat:, fix:, chore:, etc.)

**Description:**
This PR [main action]. The user will see:
- [feature 1]
- [feature 2]
- [UI states like loading, error, empty if applicable]

**Technical changes:**
- [technical change 1]
- [technical change 2]
- [technical change 3]

---

Then add a brief plain Spanish summary for reference only (no formatting, no sections, just 2-3 sentences):

*Resumen: ...*

---

Finally, analyze the changes and suggest visual resources that would be useful to include in the PR. Classify each one as:
- [NECESSARY] — the change is visual and without a reference it's hard to understand what changed
- [RECOMMENDED] — it's a new flow or module and a screenshot would add a lot of context
- [VALID] — optional but adds value (tables, data, role lists, etc.)

Format:
📎 Suggested resources for the PR:
- [CLASSIFICATION] Description of what the image or resource should show and why

If no visual resources are needed, omit this section entirely.

Rules:
- Do not generate images, tables, or any additional resources
- Do not make the PR or any git command
- Do not add explanations outside the defined format
