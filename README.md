### Danylo Mykhalchenko

Platform and backend engineer. Kyiv, Ukraine.

Thirteen years on backend services and the infrastructure that ships them. Currently building a multi-tenant SaaS platform on my own — domain model, backend, UI, containers, pipeline, deployment and the telemetry that tells me it works.

### FlowOS — in production

**https://flowos.in.ua** · live since August 2026 · a real studio running on it: https://flowos.in.ua/s/syntez

From an empty repository to production serving real users in **94 days**, solo. What is inside:

**Architecture.** Modular monolith on .NET 10, practical DDD across 18 bounded modules. Aggregates enforce their own invariants, the application layer orchestrates, the domain layer has no infrastructure dependencies. **Module boundaries are enforced by architecture tests, not by review** — a disallowed project reference fails the build. Twenty ADRs record the decisions that were expensive to reverse.

**Correctness where it is hard to get right.** Domain events are drained into an outbox table inside the same SaveChanges transaction, so an event exists if and only if its aggregate's commit did. Multi-tenancy is a hard invariant; the three deliberate exceptions are documented and guarded by a test that fails if a fourth appears quietly.

**Payments, live.** Monobank Acquiring and LiqPay — checkout, signed callbacks, refunds, idempotent webhook handling — plus PrivatBank in-person POS. Subscription billing with card-on-file, dunning and a grace window.

**Channels and integrations.** Telegram bot and Mini App with HMAC initData auth. Meta Messenger for Facebook and Instagram — passed Meta App Review. Two-way Google Calendar sync, public iCal feeds, Cloudflare R2 for media, exports and backups.

**Operations.** A single container behind a Cloudflare Tunnel — deliberately no load balancer, because Blazor Server pins a live circuit to the process that opened it. OpenTelemetry into Prometheus, Loki and Tempo. My own CI/CD with distributed build nodes and quality gates: format, lint, secret scan, build, test, coverage.

### Before that — RWS Group, 7 years

Lead developer across every product team of an enterprise localisation and content platform.

**Repository migration.** Built the automation that moved the entire product line from Bitbucket to GitHub Enterprise — alone, in three weeks, with no downtime for the ~50 engineers who depend on it. Prepare, report, wait for approval, then migrate and provision.

**Delivery.** Designed and maintained 150+ CI/CD pipelines single-handedly.

**Cloud.** Moved all 18 product services to the cloud, refactoring Windows-bound services and their build processes into Linux containers.

### Tools

.NET · C# · PostgreSQL · EF Core · Blazor Server · Podman · xUnit · Jenkins · Groovy · PowerShell · Linux · AWS · Cloudflare · OpenTelemetry

### About the graph below

Most of my work lives in private repositories, which is why the contribution graph is dense and the repository list is empty. The product above is the part you can open and use without asking me for anything.

d.mykhalchenko@gmail.com
