# Harris Punch Walk (online / sync build)

A field punch‑list tool for Harris Associates project teams. Capture punch items on a phone or
tablet — with a location dot on the room's plan and photos — then sync them to **Autodesk
Construction Cloud (ACC / Forma)** as Issues, assigned to the right subcontractor company.

Installable as an app (Add to Home Screen) and works offline for capture. Sign in with your own
Autodesk account; issues are created **as you**.

## How to use it

1. **Sign in with Autodesk** (needs internet).
2. **⚙ Setup → Load My Projects** and pick your project. Let it load members & companies.
3. Pick a floor, tap a room/area, describe the item, choose the trade, **tap the plan to drop a
   location dot** (required), add photos, and **Add**.
4. Back on internet, hit **↑ Sync Forma**. Each item becomes an ACC Issue with the correct
   subtype, company/superintendent assignment, a **location snapshot** (the plan with just that
   item's dot) plus its photos, and a due date.

Editing an item later lets you **move its dot** by tapping the plan again (it keeps its number).

## Status sync — how resolve/close flows between the app and Forma

Think of it like **passing a ball back and forth: whenever you stop, the app checks where the
ball is and matches it.** In normal use you won't be editing the same item in the app and in
Forma at the same moment, so this stays simple.

**App → Forma (push).** When you **Resolve** or **Reopen** an item in the app, the app updates
that Issue's status in Forma (**closed** / **open**) automatically:
- If you're **online**, it happens immediately (you'll see a confirmation).
- If you're **offline**, the change is saved and pushed on your next **Sync** (you'll see it
  logged in the sync window). So you don't have to close items again in Forma.

**Forma → App (reconcile on open).** Each time you open the app (online), it re‑reads the Issues
from Forma and matches each synced item's status:
- Issue **Closed** in Forma → item shows **● Resolved** in the app (and drops off the open count).
- Issue **reopened** in Forma → item goes back to **open** in the app.

**Conflict rule.** A local Resolve/Reopen that hasn't pushed yet (e.g. you did it offline) is
**protected** — the next reconcile won't overwrite it; it pushes to Forma on your next sync
instead. Once pushed, Forma is the source of truth again.

## Notes

- **Duplicates:** items already synced are skipped on future syncs, so re‑pressing Sync never
  re‑creates issues. Each synced item shows its **Forma #** and won't sync again.
- **Attachments** live in the project's Files (Docs) — that's normal ACC behavior for issue
  attachments.
- **Login** only works from this exact hosted URL (its redirect is registered with the Autodesk
  app). Open it from here, not a downloaded copy.
- **Data** is stored on your device (IndexedDB); it isn't shared between devices — Forma is the
  shared record. Each user works in their own project and won't affect others' issues.
