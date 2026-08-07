# E/E Function Allocation Rules

Use these rules after functional and logical analysis.

## Hard feasibility gates

A candidate physical node is not viable if it cannot satisfy a required constraint such as mandatory I/O/electrical interface, deterministic control-loop timing, safety independence/fault containment, availability/redundancy, compute/memory/thermal capacity, startup/wake behavior, cybersecurity boundary, or environmental/physical-location requirement.

Do not compensate for a hard blocker with a high score on cost or reuse.

## Allocation tendencies

These are heuristics, not universal rules.

### Prefer vehicle computer / HPC when
- high compute or data fusion is needed,
- functions are cross-domain,
- shared vehicle state/model is valuable,
- service reuse is strong,
- software evolution/OTA benefits from consolidation,
- physical I/O latency is not dominant.

### Prefer ZCU when
- physical I/O is geographically local,
- harness simplification matters,
- local wake/power distribution is important,
- signals are aggregated to a high-speed backbone,
- application logic can remain central while low-level I/O handling stays local.

### Prefer domain controller when
- the platform is domain-oriented or in migration,
- functions share domain-specific timing/safety resources,
- domain reuse or supplier boundaries are real constraints,
- centralization benefit does not justify migration risk.

### Prefer embedded ECU / smart actuator when
- a tight local closed-loop is needed,
- actuator-specific sensing/diagnostics/calibration are tightly coupled,
- deterministic behavior favors locality,
- fail-safe behavior must remain without upstream compute,
- physical integration/supplier module boundary is strong.

## Decision dimensions

| Dimension | Questions |
|---|---|
| Functional cohesion | Does allocation keep tightly coupled responsibility together? |
| Timing | E2E latency, jitter, scheduling, control-loop locality |
| Safety | independence, fault containment, safe state |
| Availability | redundancy, graceful degradation, single-point dependency |
| Cybersecurity | trust boundaries, exposure, privilege, secure communication |
| Compute | CPU/GPU/NPU load and future headroom |
| Memory/storage | RAM, flash/storage, logging/update headroom |
| Network | bandwidth, burst load, hops, gateway dependence |
| I/O locality | analog/discrete/PWM/sensor/actuator wiring impact |
| Power/wake | sleep current, wake source, wake latency, shutdown sequence |
| Thermal | sustained/peak compute and environment |
| Harness | length, mass, connector/pin impact |
| OTA | update unit, dependency, atomicity, rollback, compatibility |
| Diagnostics | fault ownership, observability, calibration/service boundary |
| Variants | scalability and feature/market variants |
| Reuse | carry-over platform and proven constraints |
| Supplier boundary | contract/interface stability and IP split |
| Cost | ECU/BOM/license/network/harness/manufacturing cost |
| Maintainability | change blast radius and debugging complexity |

## Qualitative comparison scale

Default if evidence is incomplete:
`BLOCKER / DISADVANTAGE / NEUTRAL / ADVANTAGE / STRONG ADVANTAGE`

Only use numeric weighting when meaningful weights exist or the user explicitly wants sensitivity analysis.

## Centralization trap checks

Before moving a function centrally, ask:
- Does raw data volume explode?
- Does actuator control become network-dependent?
- Does the function now depend on central boot/wake?
- Does a central fault disable unrelated features?
- Does OTA coupling grow?
- Are low-level diagnostics/calibration harder?
- Is the central node's safety/security partition actually available?

## Localization trap checks

Before keeping a function local, ask:
- Is vehicle-level state duplicated?
- Is the same algorithm replicated in several ECUs?
- Are cross-domain decisions delayed by gateways?
- Does local implementation create variant drift?
- Are updates fragmented across many suppliers/nodes?

## Interface realization selection

- **Direct I/O:** physical locality, deterministic control, simple low-bandwidth signals.
- **LIN:** low-cost local subnets with modest bandwidth and controlled scheduling.
- **CAN/CAN FD:** robust real-time control/status communication with bounded payload.
- **Ethernet:** high bandwidth, scalable backbone, large data flows and service-oriented systems.
- **Service-oriented interface:** consumers depend on service semantics rather than a fixed signal/frame producer.

Do not force service orientation onto tight low-level control loops merely for architectural fashion. Final choice must be based on project constraints and actual platform capability.
