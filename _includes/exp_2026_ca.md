## Culture Amp, Senior Software Engineer (Apr 2026 to present): detailed record

Senior Software Engineer on the team that builds Multi-Source Insights, the Kotlin/Ktor service AI Coach's LangGraph agent calls for turnover-risk and survey insights. This page expands the one-line bullets on the CV. Customer names, ticket references and internal identifiers are deliberately left out.

## Key responsibilities

- Drove the service's authorization model for scoped leader access, its architecture hardening, the admin configuration API, and the background-job runner's idempotency model.
- Epic owner for bringing the product into sales demo accounts, coordinating across three teams and five repositories.
- Reviewed 100+ pull requests on the insights service, plus reviews in the Rails monolith, the product's UI, the authorization-policy repository, the demo-accounts tooling and several platform repositories.
- Author of the team's design and decision records: Solution Previews, an open-questions tracker, a scored refactoring assessment, an ADR review, and an onboarding guide for Associate engineers.

## Major achievements

### 1. Designed and shipped scoped authorization for senior leaders (Jun to Aug)

- Contributed to the authorization Solution Preview and owned the open-questions tracker that resolved the role model, entitlement keys, population-scope semantics and full versus limited demographic tiers with Product, Platform Access and Security.
- Authored the service's Cerbos policy set: derived roles, shared variables, a population-scope policy and a demographic-tier policy, each with test suites.
- Delivered principal hydration from the platform's role assignments with fail-closed mapping, and the query-plan integration that pushes the viewer's scope into data access. Wrote the end-to-end test against a live policy sidecar that caught two release-blocking defects: an omitted policy version that silently denied everyone, and a query-planner-hostile policy expression that returned server errors.
- Drove the decision to route every viewer, including admins, through the policy decision point rather than special-casing locally, removing a drifting re-implementation.
- Recognised publicly by teammates for leading the Cerbos mobbing sessions.

### 2. Hardened the service architecture (Jun)

- Ran a refactoring assessment between delivery phases, published as a scored findings catalogue (architecture, backend, database, operations, QA) and turned it into a ticketed, phased backlog of pull requests under 400 lines; delegated two phases to teammates.
- Delivered the composition-root refactor: a hand-rolled application graph with no DI framework, in line with the tech radar, and fail-fast, parse-don't-validate configuration that refuses to boot while listing every error, replacing a per-request 503 ladder.
- Removed dead monitoring, metrics and request-parsing code, a shipped example file and a CI vulnerability; consolidated the account-isolation auth seam ahead of the next phase.
- Wrote analyses of a concurrency data-loss risk in admin configuration, of Kafka poison messages and offset commits, and of shared controller auth and error scaffolding.

### 3. Built the admin configuration API for analysis demographics (Jul to Aug)

- Designed and shipped the persistence layer, a demographics catalogue service, read and write endpoints for demographic tiers, a separate performance-analysis-access resource, and a lazily computed groups endpoint.
- Introduced a single access-tier vocabulary, atomic full-replace writes with catalogue validation, a fail-closed sensitivity allowlist that keeps sensitive attributes out of analysis, and column-scoped writers so two admin controls cannot overwrite each other's part of a shared row.
- Found and fixed a first-save failure caused by REPEATABLE READ snapshot isolation.

### 4. Delivered the v2 insight endpoints Coach calls as tools (Aug)

- Shipped four v2 endpoints (turnover-risk hotspots and recent survey data, each with a high-performer variant) in the insights service, plus the backing Rails endpoints, with generated OpenAPI specs; published the v2 API reference the Coach team integrates against.

### 5. Owned the sales-demo-data programme (Aug to Oct)

- Wrote the Solution Preview for derived turnover-risk demo data and its open-questions page; decided the demo-account detection mechanism and the single coarse-grained seeding endpoint shape.
- Shipped the demo-only fixture path, a demo-account flag, and cohort stubs so demo accounts return insights without configuration or policies.
- Integrated the product into the demo-accounts AWS Step Function as its own parallel branch, registered it as a flag-gated module in the demo-accounts API, added the feature flag, and configured base URLs for every development and production environment. Raised the cross-team planning dependency with the owning team.

### 6. Matured the background-job runner (Sep to Oct)

- Introduced a job-outcome contract (completed, retry later, failed) so handlers can defer or fail explicitly; moved demo seeding from an in-process waiter onto the worker; scheduled the dispatcher in production.
- Scoped and led the idempotency refactor: keyed jobs on type, entity and payload hash, grouped SQS FIFO messages by entity prefix, reverted an unsafe replace-in-flight change after review, and kept failed rows as history by rotating their key. Delegated three sub-tasks (logging, ADR refresh, failed-state handling) to teammates.
- Reviewed the FIFO-semantics ADR and the dispatcher's Datadog instrumentation; identified a merge-blocking compare-and-swap race in the watchdog and a critical runbook error during a database migration lock incident.

### 7. Developer platform and tooling

- Registered the service's OpenAPI spec in the Backstage API catalogue and fixed null-field serialization; proposed replacing the OpenAPI plugin with Ktor's native support.
- Cleaned stale CI and environment configuration across four legacy repositories.
- Built an opinionated Claude Code harness (agents, commands, skills, rules) for the team, including a Jujutsu VCS skill and a PR-size rule; wrote an agent-executable runbook for seeding the service locally.

### 8. Support and mentoring

- Wrote the team's onboarding guide for Associate engineers.
- Handled customer-facing bugs: a reporting-hierarchy issue, a snapshot-overwrite analysis with fix options for a customer, and Dutch and Portuguese translation requests.
