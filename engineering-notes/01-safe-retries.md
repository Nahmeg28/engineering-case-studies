# Retry only what's safe to retry

**Release:** 2.0.49 · **Built by:** me

## Problem

Tills on weak networks could sit on a spinner for a long time. Adding retries everywhere would have been easy, and dangerous: retrying a request that creates a sale can create it twice.

## Decision

I moved the app's networking from the basic `http` client to `dio`, with one shared configuration:

- **Explicit timeouts,** so a stalled connection ends in an error the user can act on.
- **Retries only for safe requests.** A request that creates or changes data (a POST) is never retried automatically.
- **Never retry a receive timeout.** If the request went out and the response was slow, the server may already have done the work. Sending it again is exactly how duplicates happen.
- **A local test server that stalls on purpose,** so timeout and retry behaviour could be checked without waiting for a bad network.

## Trade-off

A failed write now surfaces to the user instead of being silently retried. That is one more error message, but the user decides, and nothing is written twice. Safety for money-moving requests comes from the outbox and duplicate checks ([case study 03](../03-offline-durability.md)), not from blind retries.
