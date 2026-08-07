# Output Contract

Keep IDs stable so later revisions can be diffed.

## System Context
`SOI | Actors | Boundary | Variants | External interfaces`

## Assumption / Open-Issue Register
`ID | Type | Statement | Impact if wrong | Owner/source needed | Status`

## Scenario Table
`ID | Scenario | Trigger | Preconditions | Normal flow | Alternate/fault flow | End state`

## Function Table
`Func ID | Parent | Verb-object function | Inputs | Outputs | Modes | Timing | Failure/degraded behavior`

## Functional Chain
`Chain ID | Outcome | Ordered functions | Cross-boundary points | E2E timing | Failure path`

## Architecture Driver Register
`Driver ID | Driver | Type | Target/constraint | Source | Affected functions | Verification`

## Logical Architecture
`Logical ID | Responsibility | Functions | Provided interfaces | Required interfaces | State owner | Drivers`

## Physical E/E Allocation Matrix
`Logical/Func ID | Candidate | Feasibility | Key advantages | Key disadvantages | Selected node | Rationale`

## Interface Matrix
`IF ID | Producer | Consumer | Semantic content | Trigger/model | Timing/freshness | Fallback | Realization`

## Network Flow Table
`Flow ID | Path | Payload | Rate/event | Latency class | Hops | Protection | Load/risk`

## Timing Budget
`Chain | Stage | Sensing | Transport | Compute | Transport | Actuation/plant | Total/target`

If values are unknown, show measurement/derivation method instead of invented numbers.

## Architecture Decision Record
`ADR | Question | Alternatives | Hard constraints | Selected | Rationale | Consequences | Validation`

## Traceability Matrix
`Upstream need/req | Scenario | Function | Logical element | Physical element | Interface | Derived req | Verification`

## Architecture Risks
`Risk | Cause | Architectural impact | Detection/validation | Mitigation | Residual/open`

## Diagram conventions

Recommended Mermaid views:
1. context diagram
2. function tree
3. functional chain / sequence
4. logical architecture
5. physical E/E topology
6. critical timing sequence

Diagrams aid communication; tables remain the traceable source of truth.
