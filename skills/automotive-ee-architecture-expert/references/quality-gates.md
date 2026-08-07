# Architecture Quality Gates

## Gate 1 — Scope completeness
PASS when SOI/external boundary are explicit, variants are known or open, and external actors/interfaces are identified.

## Gate 2 — Scenario coverage
PASS when normal, key alternate/abnormal, and relevant startup/wake/sleep/shutdown/degraded/recovery cases are covered.

## Gate 3 — Functional integrity
PASS when functions are implementation-neutral, leaf functions have inputs/outputs, tree and chains agree, and critical behavior is not hidden inside ECU labels.

## Gate 4 — Architecture drivers
PASS when hard constraints are separated from preferences; timing/safety/security/availability/power/network/I/O constraints are considered; missing targets are open issues, not invented values.

## Gate 5 — Logical architecture
PASS when responsibility/state ownership are clear, arbitration points explicit, coupling intentional, and logical elements do not mirror departments.

## Gate 6 — Physical allocation
PASS when selected nodes pass hard constraints, alternatives were considered, rationale is documented, and resource/network/headroom risks are visible.

## Gate 7 — Interfaces
PASS when critical cross-boundary dependencies have semantic definitions and needed timing/freshness/fallback; realization technology does not replace semantics.

## Gate 8 — Dynamic behavior
PASS when critical chains have modes/sequences, concurrency/arbitration is covered, E2E timing is budgeted or open, and degraded behavior is architected.

## Gate 9 — Cross-cutting concerns
PASS when relevant safety, cybersecurity, diagnostics, OTA and power implications are addressed or explicitly routed to specialist analysis.

## Gate 10 — Traceability and verification
PASS when upstream needs map to functions/architecture, derived requirements identify origin, architecture-significant drivers have verification methods, and orphan requirements/elements are flagged.

## Review severity
- `BLOCKER` — architecture cannot responsibly proceed.
- `MAJOR` — material gap likely to cause redesign/integration risk.
- `MINOR` — quality/clarity issue.
- `OPEN` — missing project fact or pending decision, not automatically a defect.

## Common anti-patterns
1. PRD → ECU requirement directly, skipping functional/logical architecture.
2. Function decomposition mirrors department/ECU organization.
3. Architecture diagram drawn after decisions with no rationale.
4. Everything moved to central compute because "centralization is the trend".
5. Everything kept local because "it has always been there".
6. Interface defined only by a CAN signal name.
7. No state owner or arbitration owner.
8. Static block diagram with no timing/mode behavior.
9. Safety/security labels used without analysis.
10. Assumptions presented as platform facts.
11. Architecture optimized only for today's variant with no growth headroom.
12. ECU-count reduction that merely increases coupling and failure blast radius.
