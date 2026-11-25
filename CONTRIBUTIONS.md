# What I shipped: CNDroid POS, releases 2.0.42 – 2.0.54

CNDroid is a Flutter point-of-sale on Android fiscal devices, part of an ecosystem used by 700+ businesses in Ethiopia. From December 2025 I was its only developer, and from July 2026 its part-time lead.

**At a glance (Dec 2025 – Oct 2026)**
- **263 of the 285 commits** in releases 2.0.41 – 2.0.54 are mine.
- **All of the app's real automated tests** (about 200) were written by me. Before August 2026 it had none.
- Counts come from git history. Work that began on a colleague's branch and that I only integrated is left out of this page.

The production code belongs to my employer and stays private. This page lists features and fixes, not code.

---

| Release | Date | What I shipped |
|---|---|---|
| 2.0.42 | Jan 2026 | In-app release notes. Non-fiscal receipts and item notes on tickets. A kitchen-ticket service that avoids reprints. Payment status on document tiles. QR validation. Voucher codes from a timestamp instead of a random seed. |
| 2.0.42+1 | Jan 2026 | App updates tracked by build number. |
| 2.0.43 | Jan 2026 | Structured log files for field debugging. Kitchen-ticket lifecycle and off switch. New offline sync objects for vouchers and references. Offline "syncing" indicator. Multi-language home and menu. |
| 2.0.43+1 | Jan 2026 | Server time sync. Fiscal printer clock sync and availability check. Offline credit sales. |
| 2.0.44 | Feb 2026 | Supervisor authorization for voids. EMV and proprietary QR payment screen. Cinema QR redemption. Clock-server setting. |
| 2.0.44+1/+2 | Feb 2026 | Kitchen order-station routing. Cash sale keeps its table. QR price formatting. |
| 2.0.45 | Feb 2026 | **[E-invoice mode](07-e-invoicing-signed-qr.md)** for the Ministry of Revenues system. Article notes and modifiers restored from notes. Offline handling in voucher screens. Fix for a first-bill total mismatch in native printer code. |
| 2.0.45+1/+2 | Feb – Mar 2026 | Payment-method rules for cash sales. Price by branch. Fiscal footer after the Z report. "Print as mobile money". Reconcile tracks sync failures. |
| 2.0.46 | Mar 2026 | Duplicate bill printing. Dependency-aware reconcile sync. GPS-based customer visibility. Phone normalization for e-commerce referrals. |
| 2.0.46+1/+2 | Mar – Apr 2026 | Tool for missing shift summaries. "Printed" state for captain orders. Role-driven issuing. Online payment-processor resolution. |
| 2.0.46+3 | Jun 2026 | Fix: refunds failing to save. Line prices kept in edit mode. |
| 2.0.47 | Jun 2026 | **[Stale-edit guard](engineering-notes/02-stale-edit-guard.md)**: review before a save would drop another waiter's changes. Live captain-order settings. Employee credit limits. |
| 2.0.48 | Jun 2026 | **[Unilever integration](04-unilever-order-pipeline.md)**: orders to fiscal receipt and cash sale, automatic and manual. CO2 issue voucher. Voucher extensions with overflow prompt. Update APK chosen by device type. |
| 2.0.49 | Aug 2026 | Networking moved to `dio` with **[retries only for safe requests](engineering-notes/01-safe-retries.md)**. **Fix: duplicate sales from overlapping syncs.** Faster, visible sync. Offline screens that fail clearly instead of crashing. E-invoice A4 rendering, preview and attachment delivery. |
| 2.0.50 | Aug 2026 | Park abandoned captain orders. Search documents by any field. Voucher codes from the ERP with a local fallback. |
| 2.0.51 | Aug 2026 | **[LAN mode client](01-offline-lan-pos.md)**: keep selling through a branch PC server when the ERP is down. First ERP reachability probe. Shift periods offline. |
| 2.0.51+1 | Sep 2026 | Fix: captain order un-issued after an edit. Kitchen routing for LAN voids. |
| 2.0.52 | Sep 2026 | **[Till as local server](01-offline-lan-pos.md)** for the whole branch. **[Fix: data lost at power-off](03-offline-durability.md)** with a new encrypted SQLite store. Offline vouchers in their own tables. Keep using device data when Wi-Fi returns but the ERP is down. Android 14 foreground service. |
| 2.0.53 | Sep 2026 | **Hybrid mode**: back to the live server once it answers, device data if it dies mid-sale. Settling and closing on a till with no server. On-device server gains e-commerce orders and sales search. Kitchen display fixes. Local clock rule for sales saved away from the server. |
| 2.0.54 | Oct 2026 | **[Automatic fiscal reconciliation](05-fiscal-reconciliation.md)** with run reports. Day End no longer deletes unconfirmed sales. Steady-state outbox sync. Receipts on the built-in and network printers. **[E-invoice bill with the tax authority's signed QR](07-e-invoicing-signed-qr.md).** Electronic-journal read and print by date or range. Server parity and resilience fixes. |

---

**Write-ups:** [case studies](README.md) · [debugging notebook](06-debugging-notebook.md) · [engineering notes](engineering-notes/README.md)
