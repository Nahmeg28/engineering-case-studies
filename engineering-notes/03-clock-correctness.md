# Whose clock is right?

**Releases:** 2.0.43+1, 2.0.44, 2.0.53 · **Built by:** me

## Problem

A sale's time ends up on the fiscal receipt, in the ERP and in every report. On a fleet of Android devices, clocks drift, get set wrong by hand, or reset after a flat battery. The fiscal printer keeps its own clock too. One wrong clock puts a sale on the wrong day, which breaks daily totals and reconciliation.

## Decisions

- **Sync to the server's time.** The app reads the server's clock and works from it, instead of trusting the device.
- **Sync the fiscal printer's clock** and check that the fiscal controller is reachable, so the printer and the app agree.
- **A clock-server setting,** so a site can point at the time source it trusts, with an option to use local time where that is the right answer.
- **A clear rule for sales made away from the server.** Sales saved offline or on a branch server carry the time they actually happened, not the time they eventually synced.

## Trade-off

The app depends on one more server call and a setting to configure. In return, a sale's time is decided by a source the business controls, not by whatever the device clock says that day.
