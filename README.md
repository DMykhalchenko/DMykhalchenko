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

### The delivery platform behind it

FlowOS is built by a small team of AI agents working in parallel. That needed infrastructure of its own, so it was built alongside the product — **955 commits over the same period**, a gRPC daemon and a published CLI: 22 services, 41 background workers, 69 commands, across Domain / Application / Infrastructure layers.

**The build farm is the development machines.** Not servers — the laptops and desktops the work happens on: a 15-watt mobile i7 and a 2014 quad-core AMD APU with mixed spinning and solid-state storage. Nodes advertise what they can do, claim jobs and heartbeat; an unclaimed or stale run raises an alert. A full CI pass takes about 45 minutes, one job at a time per node. That is not slow CI — it is CI on the hardware that already exists, and the trade is visible: lose one node and a deploy waits half an hour behind the queue.

**The merge gate reads its own run table, not the provider's status API.** That is the difference that catches a green belonging to an earlier commit on the same branch, and refuses a head that no conclusive run has covered.

**It deploys and heals itself.** The daemon watches its own version drift, redeploys, repairs, and publishes its own CLI package. It also supervises the agents: stuck sessions, stalled subagents, a queue restored after a restart, a guard on the main branch.

### Before that — RWS Group, 7 years

Lead developer across every product team of an enterprise localisation and content platform.

**Repository migration.** Built the automation that moved the entire product line from Bitbucket to GitHub Enterprise — alone, in three weeks, with no downtime for the ~50 engineers who depend on it. Prepare, report, wait for approval, then migrate and provision.

**Delivery.** Designed and maintained 150+ CI/CD pipelines single-handedly.

**Cloud.** Moved all 18 product services to the cloud, refactoring Windows-bound services and their build processes into Linux containers.

### Tools

.NET · C# · PostgreSQL · EF Core · Blazor Server · Podman · xUnit · Jenkins · Groovy · PowerShell · Linux · AWS · Cloudflare · OpenTelemetry

### Code you can read

**[alloyed-devops-multitool](https://github.com/DMykhalchenko/alloyed-devops-multitool)** — adding logging, timing, retries and timeouts to legacy PowerShell automation *without editing the scripts*. It intercepts the commands a script already calls, so the script runs unmodified while every call reports itself with a correlation ID and timing.

PowerShell 7 and .NET 8. Analysis through the real PowerShell AST parser rather than regular expressions; command wrappers generated from one canonical catalog, with a CI check that fails when the generated artefacts drift; a decorator pipeline that keeps cross-cutting behaviour out of the wrapper logic; golden-file regression fixtures and ADRs for the boundaries that were expensive to reverse.

It started as a modernization proposal that was not taken up, so I built it out myself.

Most of the rest of my work lives in private repositories — which is why the contribution graph is dense and the repository list is short.

d.mykhalchenko@gmail.com · [LinkedIn](https://www.linkedin.com/in/dmykhalchenko/)
