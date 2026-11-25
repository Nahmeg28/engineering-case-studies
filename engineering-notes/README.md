# Engineering notes

Short write-ups of smaller design decisions from the CNDroid POS and the HuluBeje super-app. Each one is a single problem, the decision, and the trade-off. The longer pieces are in the [case studies](../README.md).

| Note | Theme |
|---|---|
| [Retry only what's safe to retry](01-safe-retries.md) | Networking, idempotency |
| [The stale-edit guard](02-stale-edit-guard.md) | Concurrent edits, data loss |
| [Whose clock is right?](03-clock-correctness.md) | Time on devices, fiscal data |
| [Codes that stay unique across devices](04-unique-codes.md) | Identifiers, offline generation |
| [A location bridge that never started (Bank of Abyssinia)](05-location-bridge-boa.md) | Mini-app bridges, debugging |
| [Don't let customers order what can't be served](06-open-hours-and-stock.md) | Working hours, stock rules, refactoring |
