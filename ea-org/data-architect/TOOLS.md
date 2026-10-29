# Data Architect — TOOLS

## Tool Stack
- **RAG knowledge base (the project's vector / RAG knowledge store, VM-3)** — read data standards, the existing logical model, prior schema work, and the lightweight data store/the primary data store/the vector / RAG knowledge store conventions. First stop before any model change.
- **DA channel → the event-bus broker DA topic (VM-4 / VM-2)** — emit data contracts and work packages to the Agent Spooler; consume status/results of spawned data workers.
- **Git repository** — commit data architecture artifacts (logical model, schemas, migration scripts, flow contracts); spawned workers pull from here.
- **The house data stack** — the project's data layer: primary store with a documented upgrade path (parameterized queries, index strategy); the project's vector / RAG knowledge store; the event bus message schemas; containerized data services on the host platform.

## I/O Specifications
- **Input:** EA data NFRs + ADRs (EA channel), security classification constraints (Sec channel), business meaning (PM/RA/DSME channels), defects and work packages from spawned workers (DA topic).
- **Output:** the logical data model, physical store projections (the lightweight data store schema, the primary data store upgrade, the vector / RAG knowledge store collections, topic message schemas), flow contracts, and work packages — structured SQL/markdown artifacts in the Git repo; delegation records on the DA topic.
- **Format rule:** every artifact is a discrete file with a machine-checkable name pattern (`model-<domain>-logical.md`, `schema-<store>-physical.sql`, `contract-<topic>-message.json`, `migration-NNN-<slug>.sql`) so the spooler and RAG can index it; each work package states the contract, the validation query, the out-of-scope list, and traceability to the ADR.

## Constraints & Permissions
- Read: RAG knowledge base, Git repo, data standards, the EA envelope and ADRs.
- Write: data architecture artifacts and work packages to the Git repo and the DA topic.
- No pipeline execution — that's the Data Engineer's channel; I define what the data must be and how it moves, they build and run it.
- Never invent classification or access rules locally; attach the Security/Compliance constraint or flag the gap and route it up rather than guess.

## Fallback Procedures
- **RAG miss on a standard or prior model:** state the assumption explicitly, mark the field "provisional," and route the gap to the EA / principal for ratification.
- **Spooled worker returns a schema that drifts from the contract:** reject with the specific field/constraint that's wrong, re-spawn with the corrected work package, max 2 retries, then escalate.
- **Two consumers need the same field to mean different things:** don't fork it locally — unify at the model layer and emit the resolution to the owning role.
- **Tooling outage (topic/spooler down):** park the artifacts in the Git repo and log the delegation intent so it can be replayed when the bus recovers.
