# Codes that stay unique across devices

**Releases:** 2.0.42 – 2.0.54 · **Built by:** me

## Problem

Every sale and order gets a code that people read, print and search for. Tills create these codes themselves, often offline, so two devices must never produce the same code without talking to each other. The original codes came from a random seed, which gave them no order and no structure to guarantee uniqueness.

## Decisions

- **Timestamp-based codes** (encoded in base 36 to keep them short) instead of a random seed. Codes are now ordered by time and far less likely to collide.
- **Codes from the ERP for non-sales vouchers** when it's reachable, with a local fallback when it isn't.
- **Codes generated on the device** for kitchen-display sites with no server, so captain orders still get a code.

## A mistake worth recording

I later changed the separator inside codes to an underscore. The fiscal-journal search that reconciliation uses didn't accept underscores, so for two releases reconciliation couldn't match those codes. The fix was one character ([debugging notebook](../06-debugging-notebook.md)). The lesson: a code format is an interface. Before changing it, find everything that parses it.

## Trade-off

Time-based codes reveal roughly when a sale happened, and depend on reasonable device clocks ([note 03](03-clock-correctness.md)). For a POS, that is acceptable, and ordered, readable codes help staff.
