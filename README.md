# Harris Punch Walk (online / sync build)

A field punch‑list tool for Harris Associates project teams. Capture punch items on a phone or
tablet — each pinned to a **location dot** on the plan, with photos — then push them to
**Autodesk Construction Cloud (ACC / Forma)** as Issues, assigned to the right subcontractor or
superintendent.

Installable as an app (**Add to Home Screen**) and works **offline** for capture. You sign in
with **your own Autodesk account**, so issues are created **as you** (not a service account).

## How to use it

1. **Sign in with Autodesk** (needs internet the first time).
2. **⚙ Setup → Load My Projects** → pick your project → **Load Members & Companies**.
3. Pick a floor, tap a room/area, write the item, choose the trade, **tap the plan to drop a
   location dot** (required — you can't Add without one), add photos, and **Add**.
4. Back online, hit **↑ Sync Forma**. Each item becomes an ACC Issue with:
   - the correct **issue type/subtype**,
   - **assignment** (subcontractor company, or the **superintendent** for General items),
   - a **location snapshot** (the plan with *just that item's* dot) attached first, then its photos,
   - and a **due date**.

Editing an item lets you **move its dot** by tapping the plan again (it keeps its number).

## Sync

- **Fast:** items and photos upload **in parallel**, so a full floor syncs in a couple minutes
  rather than 10–15.
- **No duplicates:** already‑synced items are skipped — re‑pressing Sync never re‑creates them.
  Each synced item shows its **Forma #**.
- **Clear errors:** the sync log names the exact issue/photo and the API response if anything fails.

## Status sync — resolve/close flows both ways

Think of it like **passing a ball back and forth: when you stop, the app checks where the ball
is and matches it.** You won't normally edit the same item in the app and in Forma at once, so
it stays simple.

- **App → Forma:** **Resolve/Reopen** in the app closes/reopens the real Forma issue —
  immediately when online, or on your next **Sync** if offline. No need to close items again in Forma.
- **Forma → App (on open):** the app re‑reads Forma and matches status — **Closed → ● Resolved**,
  **reopened → open** (room counts update to match).
- **Conflict rule:** a local change you made offline is **protected** and pushed on next sync —
  the reconcile won't overwrite it until it's in Forma.

## Backup & Restore (⚙ Setup → Backup & Restore)

Protects work that hasn't synced yet and lets you continue on another device.

- **Where:** a **`Punchlist_Tool_backup`** folder in the project's **Files**, with a **dated
  sub‑folder per day** (`YYYY‑MM‑DD‑punchwalk_backup`) holding that snapshot. The folder is
  **locked to Project Admin / Manager / Engineer** roles so subs can't see it.
- **What:** all item data + photos for **un‑synced** work (synced work is already safe in Forma).
- **Auto:** runs after every sync. **Manual:** **↑ Back up now** anytime.
- **Restore:** **↓ Restore from ACC** → if there are several dated backups you pick which one →
  it **replaces** this device's list with that snapshot. Newest date = most complete; older = a rollback.
- **Cross‑device:** sign in on any device, load the project, and Restore to pick up where you left off.

## Notes

- **Login** only works from this exact hosted URL (its redirect is registered with the Autodesk
  app). Open it from here — not a downloaded copy.
- **On‑device storage:** items and photos live in the browser's IndexedDB. It isn't automatically
  shared between devices — **use Backup/Restore** (above) or Forma as the shared record.
- **Switching projects:** the device keeps your current items until you **Restore** the new
  project's backup (which replaces the list) — so restore first when you move to another project.
- **Attachments** live in the project's Files (Docs) — normal ACC behavior for issue attachments.
- **Notifications:** creating/assigning issues (and status changes) can trigger ACC's normal
  notifications to assignees/watchers, per issue. That's controlled by ACC/user notification
  settings, not the app.

## Files in this repo

`punch-tool.html` (the whole app) · `sw.js` (offline service worker) · `manifest.json` · icons ·
`floor-plans/complete/` (per‑floor plan images).
