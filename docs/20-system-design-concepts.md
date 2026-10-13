## 20. System design concepts

**How to approach any design problem**

1. **Clarify requirements:** functional (what it does) and non-functional (scale, latency, availability, security, cost, accessibility, i18n).
2. **State assumptions and constraints:** users, traffic, data size, team size, deadlines, existing stack.
3. **Sketch the high-level design:** clients, services, data stores, third parties.
4. **Define the data model and the API/interfaces.**
5. **Deep-dive the risky parts:** bottlenecks, failure modes, consistency, security.
6. **Discuss trade-offs out loud.** There is no best design, only a design that fits the constraints.

For frontend design problems, a handy checklist is **RADIO:** Requirements, Architecture, Data model, Interface (API), Optimizations.

**Networking and communication**

- Client-server model, HTTP/1.1 vs HTTP/2 vs HTTP/3, HTTPS/TLS, DNS, CDN, proxies and reverse proxies, load balancers.
- API styles: **REST**, **GraphQL**, **gRPC**, **WebSocket** (bidirectional real time), **Server-Sent Events** (server to client stream), **long polling**, **webhooks**.
- **Pagination:** offset (simple, slow on large sets, unstable with changes) vs cursor/keyset (stable and fast).
- **Idempotency:** the same request repeated has the same effect; use idempotency keys for payments and creates.
- **Retries with exponential backoff and jitter**, timeouts, **circuit breakers**, **rate limiting**, **backpressure**.

**Data and storage**

- SQL (relations, transactions, joins) vs NoSQL (document, key-value, wide-column, graph). Choose by access patterns.
- **Indexes** speed reads and slow writes. **Replication** gives availability and read scale. **Sharding/partitioning** gives write and storage scale.
- **ACID** (strong guarantees) vs **BASE** (availability, eventual consistency).
- **CAP theorem:** under a network partition you choose consistency or availability. **PACELC** adds the latency trade-off when there is no partition.
- **Consistency models:** strong, eventual, read-your-writes. In UIs this appears as optimistic updates and stale data.
- **Caching layers:** browser, service worker, CDN, application, database. Strategies: cache-aside, write-through, write-behind. Invalidation is the hard part; use TTLs and tags.
- Blob/object storage for files, search engines for text search, time-series stores for metrics.

**Architecture styles**

- **Monolith, modular monolith, microservices.** Start with a modular monolith unless you have a clear reason to split; microservices trade simplicity for independent scaling and deployment.
- **Event-driven architecture:** message queues, pub/sub, streams; **CQRS** (separate read and write models), **event sourcing**, **saga** pattern for distributed transactions.
- **API gateway / BFF (backend for frontend):** a backend tailored to one client, so the frontend does less stitching.
- **Stateless services** scale horizontally; keep state in stores.
- **Vertical vs horizontal scaling**, autoscaling, containers, orchestration, serverless.
- **12-factor app:** config in the environment, logs as streams, disposable processes, dev/prod parity.

**Reliability and operations**

- Availability expressed in nines (99.9 percent is about 8.8 hours of downtime per year), **SLI/SLO/SLA**, latency percentiles (p50, p95, p99), error budgets.
- **Observability:** logs, metrics, traces; dashboards and alerts that matter.
- Deployment strategies: **blue-green**, **canary**, **rolling**, **feature flags**, quick rollback.
- **Infrastructure as code**, environments (dev, staging, prod), secrets management.
- **Disaster recovery:** backups, RPO (how much data you can lose) and RTO (how long you can be down).

**Security and identity**

- Authentication vs authorization; sessions vs tokens; **JWT** (and its revocation problem), **OAuth 2.0 / OpenID Connect**, SSO, MFA; **RBAC** vs **ABAC**; least privilege; secrets rotation.

**Frontend system design topics**

- **Rendering strategies:** CSR, SSR, SSG, ISR, streaming SSR, islands, and when each fits (SEO, time to first byte, interactivity, cost).
- **Micro-frontends** (module federation, iframes, web components): independent deployment for large organizations; costly in complexity and bundle duplication. Do not adopt without a clear need.
- **State architecture:** server state vs client state vs URL state (section 9).
- **Caching and offline:** HTTP caching, service workers, PWA, optimistic updates, retry queues.
- **Real time:** WebSocket vs SSE vs polling; reconnection and ordering.
- **Large data:** virtualization, pagination, web workers for heavy computation.
- **Auth flows:** token refresh, silent re-auth, protected routes, logout everywhere.
- **Uploads:** chunked and resumable uploads, progress, validation.
- **Internationalization and RTL**, accessibility, analytics, error monitoring, feature flags, A/B testing, design system and tokens.
- **Build and delivery:** bundling, code splitting, tree-shaking, CDN, cache busting with content hashes.

**Fallacies of distributed computing (Deutsch):** assuming the network is reliable, latency is zero, bandwidth is infinite, the network is secure, topology never changes, there is one administrator, transport cost is zero, and the network is homogeneous. Design for the opposite.
