# Engineering case studies

Architecture write-ups of production systems I built or re-architected as a mobile engineer at Red Cloud ICT Solutions (Addis Ababa).

The production code belongs to my employer and stays private. These documents cover what I'm free to share: the problem, the constraints, the architecture, the decisions and trade-offs, and what I'd do next. No proprietary code, schemas, endpoints or client data appear here.

| # | Case study | App | Themes |
|---|---|---|---|
| 01 | [Selling through outages: offline and LAN mode for a production POS](01-offline-lan-pos.md) | CNDroid POS (Flutter, Android) | Offline-first, encrypted SQLite, on-device HTTP server, sync, concurrency |
| 02 | [Routing that doesn't strand drivers: dual-provider fallback](02-dual-provider-routing.md) | HuluBeje Delivery (Flutter) | Resilience, retry with backoff, caching, provider abstraction |

More to come: e-invoicing for the Ministry of Revenues system, and integrating a super-app as a mini-app inside a bank's app.
