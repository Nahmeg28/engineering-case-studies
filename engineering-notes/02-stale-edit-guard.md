# The stale-edit guard

**Release:** 2.0.47 · **Built by:** me

## Problem

In a restaurant, a table's open order ("captain order") is edited by several people on several tills. A waiter opens the order, a colleague adds items on another till, and the first waiter saves. The first waiter's copy is out of date, so saving it could quietly drop the colleague's items.

## Decision

Before saving, the app fetches the server's current copy of the order and compares it with the local one. If saving would **remove or change** anything the server has (items, quantities, notes or header fields), the waiter sees a review screen listing those differences before anything is overwritten.

The branch server used in LAN mode goes one step further, with a version number on every order: a stale save is rejected outright and the till must reopen the order ([case study 01](../01-offline-lan-pos.md)).

## Trade-off

The check adds one server request to every save, and sometimes one extra screen. In return, the order on the table always matches what the kitchen is cooking, and nobody loses items without seeing it happen.
