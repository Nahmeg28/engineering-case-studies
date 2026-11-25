# Debugging notebook: five production bugs in a POS

**App:** CNDroid POS, a Flutter point-of-sale on Android fiscal devices
**My role:** I found and fixed each bug below (releases 2.0.46 – 2.0.54). Two of them I had caused myself, and I say so.

Each entry follows the same shape: what users saw, the root cause, the fix, and how it was verified.

---

## 1. Local data lost at power-off

- **Symptom:** unsynced sales and downloaded data disappeared when a device was switched off.
- **Root cause:** the storage wrapper called the key-value store's write without awaiting it. Every "awaited" save returned before the data was committed. The safety record written before each fiscal print used the same path.
- **Fix:** a new encrypted SQLite store whose writes return only after commit, a streamed one-release migration, and a degraded mode if the database can't open.
- **Verified by:** 15 tests on the store and one migration-compatibility test.
- **Lesson:** an `await` on the caller's side proves nothing if the callee doesn't await. Read the storage layer, not just its signature.

Full write-up: [case study 03](03-offline-durability.md).

## 2. Duplicate sales from overlapping syncs

- **Symptom:** the same sale appeared twice in the ERP after network drops.
- **Root cause:** two faults together. The connectivity listener fired on every reconnect, so a flapping link started a second sync while the first was mid-flight, and both read the same pending list. And the offline flag was cleared *after* the sync started, so it ran against cached data.
- **Fix:** a one-run-at-a-time guard, released in `finally`, and clear the flag before syncing. A later release extended the guard to the manual "sync now" path, which the first fix had missed.
- **Lesson:** list every entry point into a critical section before declaring a race fixed.

## 3. Day End deleting sales the printer couldn't confirm

- **Symptom:** Day End could delete the on-device record of a sale the printer hadn't confirmed.
- **Root cause:** when the fiscal-journal search failed or found nothing, the old code deleted the on-device safety record anyway, sometimes the only record of the sale. A single try block around the whole loop also meant one bad entry, such as an unparseable date, stopped everything after it.
- **Fix:** keep entries that can't be confirmed, give each entry its own error handling, and log every outcome.
- **Lesson:** "not found" and "doesn't exist" are different answers. Never delete on an inconclusive check.

## 4. Reconcile re-sending a sale that reached the server mid-run

- **Symptom:** a sale could be posted by reconciliation after the normal sync had already posted it.
- **Root cause:** check-then-act. Reconcile built its "already on the server" list at the start, then worked through files one by one while the outbox kept posting in parallel.
- **Fix:** re-check each sale just before posting; if it's already there, skip it and clean up.
- **Lesson:** a snapshot taken at the start of a long job goes stale. Check again at the point of action.

Full write-up: [case study 05](05-fiscal-reconciliation.md).

## 5. Refunds failing to save (a bug I introduced)

- **Symptom:** refunds failed with a generic "error while saving the voucher".
- **Root cause:** when building print data, I had placed a `return` inside a branch that only covered cash and credit sales. Refunds fell through to an older bare `throw`, and the catch block above replaced it with the generic message, hiding the real cause. Refunds stayed broken for a few releases.
- **Fix:** return for every voucher type, rethrow the original error instead of masking it, and show a separate message when the user cancels a QR payment.
- **Lesson:** generic error messages turn a five-minute bug into a multi-release one. Keep the original error, and test the less common paths, not just cash sales.

---

## Shorter ones

- **A one-character regression (mine).** I changed the voucher code separator to an underscore; the fiscal-journal search pattern didn't allow underscores, so reconciliation couldn't match those codes for two releases. Fixed by allowing the character, and a reminder to search for every consumer of a format before changing it.
- **First bill's total didn't match.** The native bill code recomputed the total from rounded line prices with a fixed tax rate. It now prints the total the app already calculated, so there is only one source of truth.
- **A finished kitchen order reappearing on screen.** Rebuilding the line items dropped the fields that mark them done. Fixed by carrying those fields through the rebuild.
- **An order losing its "issued" state after an edit.** The edit recomputed the state from the current workflow step instead of keeping it. Fixed by preserving it.
