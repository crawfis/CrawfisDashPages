# UGS Infinite Runner — Kanban (GitHub Pages)

Single-file, client-side **Kanban board** for the UGS Infinite Runner project.  
Includes `localStorage` persistence + JSON **Export/Import**. Ideal for GitHub Pages.

## Quick Deploy (GitHub Pages)
1. Create a new repo (e.g., `ugs-kanban`).  
2. Add the file: `index.html` (use the provided `ugs_infinite_runner_kanban.html`, rename to `index.html`).  
3. Push to `main`.  
4. Repo **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main` → Folder: `/root`.  
5. Open the Pages URL. Your board loads with **localStorage** persistence (per browser/device).

## Features
- P0/P1/P2 priority filter (swimlanes).
- Status columns: To Do, In Progress, Blocked, Done.
- Owner tags: Backend / Client / Data-QA / Ops.
- Search filter.
- **Export/Import** tasks as JSON.
- **localStorage** persistence (same device/browser).

## Limitations
- No server sync. To move between devices, use **Export/Import**.
- If you change the domain/repo name, localStorage data will not carry over.

## File Map
- `index.html` — Single-file React app (CDN-loaded) with Tailwind.

## Maintenance
- To reset to seed tasks: click **Reset** in the header.
- To back up: **Export** → saves `kanban_tasks.json`.  
  To restore: **Import** → choose a previously exported JSON file.

## Prompt Library (for Copilot/LLMs)
Use this **Master Context Pack** + prompts for consistent output across stories/tasks.

### Master Context Pack (prepend to every prompt)
```
PROJECT: Infinite Runner using Unity Gaming Services (UGS).
GOALS:
- Cloud Save: profile/progression, personal leaderboards (lifetime/weekly/monthly), 12-week history.
- Leaderboards: Weekly tiered (Bronze/Silver/Gold/Platinum, threshold-based), Monthly tiered (phase 2), Lifetime global.
- Economy: server-authoritative coins/gems, daily/weekly rewards via Cloud Code only; Cloud Save holds non-authoritative mirrors for UI.
- Anti-cheat: all writes go through Cloud Code; distance/duration sanity; per-run coin caps; one submission per run; metadata requirements.
- Resets: Weekly Mon 00:00 UTC; archive personal weekly to 12 entries; demote/promote by thresholds.
- UX: personal bests, tier badge, countdown; Kanban tasks tracked in this chat’s canvas “UGS Infinite Runner — Kanban”.
DECISIONS (LOCKED):
- 4 tiers; threshold promotion; personal history depth 12 weeks; leaderboard entries carry metadata (distance, duration, characterId, runVersion).
ACCEPTANCE PRINCIPLES:
- Cross-device persistence; no client-authoritative economy; leaderboards reflect correct tier; reset accuracy; <1% false positives on anti-cheat.
REFERENCES:
- Plan PDF in chat (“UGS Infinite Runner Plan (Decisions & Execution)”).
- Canvas Kanban in this chat: “UGS Infinite Runner — Kanban”.
```

### Prompts (pick one per task)
- **User Story Kickoff**: Create story, AC, non-goals, dependencies, risks, estimates.
- **Task Breakdown**: Table of tasks with owners/priority/status, sequencing, test cases, telemetry.
- **Cloud Code Spec**: Inputs, validations, side effects (Cloud Save/Economy/Leaderboards), errors, rate limits, observability, security, acceptance tests.
- **Anti-Cheat Rule Update**: Signals, rules, actions, safeguards, QA scenarios.
- **Leaderboard/Tier Change Ticket**: Change summary, affected boards, rollover, migration, comms, rollback.
- **Economy/Reward Flow**: Reward table, call path, idempotency, limits, acceptance, analytics.
- **UX Copy + Telemetry**: Microcopy, edge states, countdowns, accessibility, telemetry fields.
- **Test Plan Slice**: Scope, envs, boundary matrix, negative tests, perf targets, sign-off.
- **Risk Review**: Top risks, runbooks, mitigation readiness, Go/No-Go checklist.
- **Kanban Sync Helper**: Return diffs to update the canvas Kanban (ID → new status/owner/priority, rationale).

> Tip: Keep prompts concise and always paste the **Master Context Pack** first.
