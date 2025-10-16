# UGS Infinite Runner — Kanban (GitHub Pages + localStorage Only)

**Generated:** 2025-10-16 16:13 UTC

## Scope
- This guide covers **only** the standalone GitHub Pages board (single-file HTML) with `localStorage` persistence.
- Canvas/editor variants are out of scope.

## Manual Updates (on GitHub Pages)
1. **Change Status/Owner**  
   Open your Pages URL. Use the dropdowns on each card. Changes auto-save to `localStorage` on that device/browser.
2. **Filter & Search**  
   Priority (P0/P1/P2/All), Owner (Backend/Client/Data/QA/Ops), and search box to narrow results.
3. **Backup / Migrate**  
   **Export** → downloads `kanban_tasks.json` (your current board state).  
   **Import** → select a prior JSON to restore.
4. **Bulk Edit Tasks via JSON**  
   **Export** → edit the JSON in a text editor (IDs are unique).  
   **Import** the updated JSON.  
   **Task object shape:**  
   `id` (string), `title` (string), `desc` (string), `owner` ∈ {Backend, Client, Data/QA, Ops}, `priority` ∈ {P0,P1,P2}, `status` ∈ {To Do, In Progress, Blocked, Done}
5. **Update the App Itself (`index.html`)**  
   Clone/pull your repo, edit `index.html`, commit/push to `main`. GitHub Pages redeploys automatically.

## Common Ops
- **Reset to seed tasks:** click **Reset** (if present) or re-upload a clean `index.html`.
- **Move to a new repo/domain:** **Export** JSON first; `localStorage` does **not** transfer across domains.

## Validation Tips
- After bulk edits, scan columns for obvious misplacements.
- Keep IDs stable; changing an ID creates a new task.
- If import fails: validate JSON syntax and required fields.

---

## Prompts (for ChatGPT/Copilot)

### A) “Kanban Sync” (modify task states via JSON roundtrip)
Use when you want help editing your board’s task list. Paste your exported JSON and the desired changes; get back a corrected JSON to **Import**.

**Prompt**  
```
You are updating a GitHub Pages single-file Kanban for the UGS Infinite Runner project. The board persists to localStorage and supports Export/Import of a tasks JSON array.

Task:
- Apply the following changes by task ID (status/owner/priority/title/desc).
- If an ID doesn’t exist, append a new task object.
- Validate fields: owner ∈ {Backend, Client, Data/QA, Ops}; status ∈ {To Do, In Progress, Blocked, Done}; priority ∈ {P0,P1,P2}. If invalid, correct and report.
- Return ONLY the full, updated JSON array (no extra text).

Input:
1) Current tasks (paste JSON array here).
2) Requested changes (bullets).

Output:
- The updated JSON array to save as kanban_tasks.json and Import back into the board.
```

### B) “Structural Change Spec” (ask for code edits to `index.html`)
Use when you want to change the app (new owners/statuses, new fields, etc.). You’ll receive a small diff/code block to paste into `index.html`.

**Prompt**  
```
I’m hosting a single-file Kanban on GitHub Pages with localStorage persistence. Propose minimal code changes to index.html to implement:

- <List your structural changes: e.g., add Owner “Design”, add Status “Review”, make P0 default filter, add Export/Import/Reset buttons if missing>
- Keep styling simple; do not introduce external build steps.
- Provide a concise code diff or replacement snippets and identify the exact locations (by constants or function names).
- No backend; all persistence must remain in localStorage.
```
