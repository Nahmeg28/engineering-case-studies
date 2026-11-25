# Don't let customers order what can't be served

**App:** HuluBeje, a Flutter consumer super-app · **Releases:** 2.0.10+122 (Sep 2025) and 2.1.7+145 (Apr 2026) · **Built by:** me, on top of an open/closed flag and a delivery-only hours check that colleagues built earlier

## Problem

Customers could schedule pickup or dine-in for a time when the branch was closed, because only delivery checked working hours. And restaurants had no stock enforcement: a customer could add and pay for an item the kitchen had run out of. Staff then had to call the customer or cancel.

## Decisions

**1. One scheduler for every serving method (Sep 2025).**
I moved the working-hours check out of the delivery screen into a shared helper, and applied it to pickup and dine-in too. Each weekday has its own hours, with a safety buffer at the start and end, and a closed branch can only take scheduled orders. Time comes from the server, with the phone clock only as a fallback, so a wrong phone clock can't open a closed branch.

I then merged two serving-method view models into one shared selector. One of the two I deleted was my own, written five days earlier. Keeping both would have meant two copies of the same rules, so the earlier design had to go.

**2. Stock-aware ordering for restaurants (Apr 2026).**
For restaurants with stock control switched on:
- Out-of-stock items are greyed out and can't be added.
- Low-stock items show a warning and "N left", and the quantity is capped at what's available.
- Staff can switch an item off while it's still in stock, for example when a machine is broken. The customer sees "disabled", not "out of stock".

Other industries keep their old behaviour, and the low-stock level is a server setting the business can tune without a release.

**3. Choose, then continue (Apr 2026).** Tapping a serving method used to move on at once. Now the customer picks one, and Continue stays off until they have, so nobody moves on without a method chosen.

## Trade-offs

- **Stock is as fresh as the last menu load.** Feedback is instant while browsing, but two customers can still both take the last portion.
- **Two stock rules now live side by side:** restaurants with stock control, and everyone else.

## What I'd do next

- **Re-check stock when adding to cart,** and again at checkout.
- **Put the stock rule in one policy class.** It is currently repeated in five places (cart, item screen, add button, item tile), and copies drift.
- **Match working hours by typed weekday values,** not English day names.
