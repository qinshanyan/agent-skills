# Architecture Method Reference

## Layer model

This skill uses a pragmatic automotive adaptation of MBSE/Arcadia-style separation:

| Layer | Main question | Typical artifacts |
|---|---|---|
| Operational / Context | Why and in what scenario? | actors, scenarios, boundary |
| System Functional | What must the vehicle/system do? | function tree, functional chains |
| Logical | How should responsibilities be grouped independent of actual ECU? | logical elements/interfaces |
| Physical E/E | Where is it realized? | HPC/ZCU/ECU/sensor/actuator allocation, topology |
| Realization boundary | What HW/SW/interface requirements follow? | derived requirements, downstream allocation |

A lower layer must not silently rewrite the intent of the upper layer.

## Static and dynamic views

A complete architecture normally needs both.

**Static:** elements, responsibilities, interfaces, relationships, physical allocation, topology.

**Dynamic:** modes/states, sequences, timing, concurrency, arbitration, failure/degraded behavior.

Automotive SPICE 4.0 SYS.3 distinguishes static and dynamic aspects of the system architecture and expects architecture analysis, rationale, consistency and bidirectional traceability. Use these ideas as quality gates rather than as a compliance checklist.

## Functional decomposition heuristics

Good decomposition:
- preserves user/system intent,
- removes implementation assumptions,
- uses verb-object function names,
- separates sensing / interpretation / decision / coordination / actuation when they are genuinely independent responsibilities,
- exposes cross-domain dependencies,
- stops before source-code design.

Bad decomposition:
- BDC function / VCU function / cockpit function as first-level branches,
- "send CAN signal" as a vehicle function,
- one function per department,
- splitting until every function is a runnable regardless of architecture value.

### Example

`Provide automatic tailgate closing`
→ detect close request
→ validate operation conditions
→ plan closing action
→ command drive movement
→ monitor position/speed
→ detect obstruction
→ coordinate latch/cinch
→ report state to user
→ enter degraded/recovery behavior

Only after this should the architect decide what belongs to BDC, tailgate ECU, latch ECU, central computer or zone controller.

## Functional chain

A function tree answers **what functions exist**. A functional chain answers **how an outcome is delivered**.

Capture source/trigger, transformations/decisions, state owner, final actuator/output, timing budget, failure propagation and cross-node boundaries.

## Logical grouping

Prefer grouping by common state ownership, shared timing/control loop, high internal interaction, common safety/security boundary, and coherent lifecycle/update boundary. Do not group merely because functions currently live in the same ECU.

## Architecture pattern vocabulary

- **Distributed / embedded:** many local ECUs execute domain/application logic near sensors/actuators.
- **Domain:** functions are consolidated by functional domain.
- **Centralized / vehicle computer:** cross-domain application logic is consolidated into fewer high-performance computers.
- **Zonal:** physical I/O aggregation/local services are organized by vehicle location/zone, often with high-bandwidth backbone links to central vehicle computers.
- **Hybrid:** production platforms may mix legacy ECUs, domains, central computers and ZCUs. Treat migration as a constrained architecture, not a clean-sheet diagram.

## Architecture analysis questions

- Does it satisfy all hard functional/non-functional constraints?
- What fails together?
- What must boot/wake together?
- What must update together?
- What data crosses network boundaries and why?
- What is the worst gateway/path dependency?
- Where is authoritative state stored?
- Where is arbitration performed?
- Can variants reuse the design?
- What happens if one node is unavailable?
- Is diagnosis possible at the chosen boundary?
- Does the architecture reduce or merely relocate complexity?
