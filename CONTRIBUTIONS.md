# What I shipped

Release-by-release record of my work on three production Flutter apps at Red Cloud ICT Solutions (Addis Ababa), part of an ecosystem used by 700+ businesses in Ethiopia. Counts come from git history. Work that began on a colleague's branch and that I only integrated is left out.

The production code belongs to my employer and stays private. This page lists features and fixes, not code.

- [CNDroid POS](#cndroid-pos-releases-2042--2054)
- [HuluBeje (consumer super-app)](#hulubeje-consumer-super-app)
- [HuluBeje Delivery (driver app)](#hulubeje-delivery-driver-app)

---

## CNDroid POS, releases 2.0.42 – 2.0.54

A Flutter point-of-sale on Android fiscal devices. From December 2025 I was its only developer, and from July 2026 its part-time lead.

**At a glance (Dec 2025 – Oct 2026)**
- **263 of the 285 commits** in releases 2.0.41 – 2.0.54 are mine.
- **All of the app's real automated tests** (about 200) were written by me. Before August 2026 it had none.

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

## HuluBeje (consumer super-app)

A Flutter app for ordering food, booking cinema and more, with 60K+ downloads on Google Play and the App Store. It also runs as a mini-app inside telebirr and Bank of Abyssinia's app. After the senior developer left, I was the main contributor and put out five releases (2.0.11+138 to 2.1.7+145, March – April 2026).

**At a glance (Aug 2025 – Apr 2026):** 81 commits under my name. The mini-app framework, the telebirr integration and the payment flow were built by others before me.

| Period | What I shipped |
|---|---|
| Aug 2025 | Reworked the customer side of an **ultrasonic "sonic redeem"**: one message format shared by the sound and the encrypted order QR, and a guard against repeat taps. (The feature was later switched off after the sound library crashed on some devices.) Support call button and supervisor name in the order activity log. |
| Sep 2025 | **[One serving-method selector with working-hours scheduling](engineering-notes/06-open-hours-and-stock.md)** for delivery, pickup and dine-in. Invitation notifications with invitee name auto-fill. Skip-table option controlled by a setting. Cinema calendar button. |
| Oct 2025 | Photo upload on driver reviews and a clearer delivery route panel. Android 13+ photo permissions. Paged notifications with pull-to-refresh. Settings-driven feature toggles. |
| Nov – Dec 2025 | Cinema closed-show state and time-format fixes. Small usability fixes. |
| Feb 2026 | **[Bank of Abyssinia: bank-validated single sign-on](engineering-notes/05-location-bridge-boa.md)** that fails closed with a clear reason, tested with the bank's team. |
| Mar 2026 | **[Change an order after payment](08-change-order-after-payment.md)**: six dine-in, pickup and delivery switches, address change, server-priced previews and linked history. Restaurants sorted by the customer's location. Releases 2.0.11+138 to 2.1.7+143. |
| Apr 2026 | **[Bank of Abyssinia: location bridge fix](engineering-notes/05-location-bridge-boa.md)**. **[Stock-aware ordering](engineering-notes/06-open-hours-and-stock.md)** for restaurants. Choose-then-continue serving selection. Read-only driver review in order history. Release 2.1.7+145. |

---

## HuluBeje Delivery (driver app)

A Flutter app for delivery drivers, first built in 2023. I extended it from November 2025 and was its primary contributor after the senior developer left.

**At a glance (Nov 2025 – Apr 2026):** 26 of the 31 non-merge commits in that window are mine, and about 29% of the app's current code.

| Area | What I built |
|---|---|
| **In-trip order changes** | The app now notices when a customer cancels or changes the address mid-trip: it clears cancelled orders, re-routes and updates the ETA. Before, it stopped listening once a driver accepted an order. |
| **[Dual-provider routing](02-dual-provider-routing.md)** | Turn-by-turn routes with a primary and a backup provider, retry with backoff and jitter, a per-order route cache, and a remote switch. |
| **Reliable driver actions** | Only one action runs at a time across 8 driver actions, failures are typed (timeout, network, server, business, validation) with clear messages, and 7 actions offer one-tap retry. |
| **Location and connectivity health** | Detects quiet GPS, location turned off or denied, and lost internet, and tells the driver. Automatic arrival at the branch and the customer within a server-set radius. |
| **Commission earnings** | A reward alert after a trip and an earnings summary (client side). |
| **Trip flow and details** | Hardened the existing trip steps with timeouts and error handling. Order line items and tap-to-call on the request sheet. Driver stats on the profile. Photo, battery and location on status reports. |

---

**Write-ups:** [case studies](README.md) · [debugging notebook](06-debugging-notebook.md) · [engineering notes](engineering-notes/README.md)
