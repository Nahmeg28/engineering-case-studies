# Engineering case studies

Architecture write-ups of production systems I built or re-architected as a mobile engineer at Red Cloud ICT Solutions (Addis Ababa).

The production code belongs to my employer and stays private. These documents cover what I'm free to share: the problem, the constraints, the architecture, the decisions and trade-offs, and what I'd do next. No proprietary code, schemas, endpoints or client data appear here.

| # | Case study | App | Themes |
|---|---|---|---|
| 01 | [Selling through outages: offline and LAN mode for a production POS](01-offline-lan-pos.md) | CNDroid POS (Flutter, Android) | Offline-first, encrypted SQLite, on-device HTTP server, sync, concurrency |
| 02 | [Routing that doesn't strand drivers: dual-provider fallback](02-dual-provider-routing.md) | HuluBeje Delivery (Flutter) | Resilience, retry with backoff, caching, provider abstraction |
| 03 | ["Saved" should mean saved: offline mode that survives power cuts](03-offline-durability.md) | CNDroid POS | Durability, encrypted SQLite, migration, mode switching, sync races |
| 04 | [From a Unilever order to a fiscal receipt, unattended](04-unilever-order-pipeline.md) | CNDroid POS | Third-party integration, polling, fiscal hardware, partial failure |
| 05 | [Making the fiscal printer and the ERP agree](05-fiscal-reconciliation.md) | CNDroid POS | Data consistency, decision tables, race conditions |
| 06 | [Debugging notebook: five production bugs](06-debugging-notebook.md) | CNDroid POS | Root-cause analysis, including two bugs I caused |

**Everything I shipped, release by release:** [CONTRIBUTIONS.md](CONTRIBUTIONS.md)

More to come: e-invoicing with the tax authority's signed QR, HuluBeje inside Bank of Abyssinia's app, and short engineering notes.
