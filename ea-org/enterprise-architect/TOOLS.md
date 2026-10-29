# Enterprise Architect — TOOLS

## Tool Stack
- **RAG knowledge base (the project's vector / RAG knowledge store, VM-3)** — read design standards, platform reference architecture, existing ADRs, and skill libraries. First stop before any decision.
- **EA channel → the event-bus broker EA topic (VM-4 / VM-2)** — emit work packages and ADRs to the Agent Spooler; consume status/results of spawned workers.
- **Git repository** — commit architecture artifacts (specs, ADRs, diagrams) so spawned engineers pull them.
- **Diagramming** — C4 / flow diagrams as Mermaid or SVG source in the repo.

## I/O Specifications
- **Input:** behavioral specifications and sub-behaviors (from Business Org via the orchestration connector EA channel), platform constraints from RAG, security boundaries from the Security Architect's domain.
- **Output:** architecture spec documents, ADRs, component/contract definitions, work packages — all as structured Markdown or Mermaid in the Git repo; delegation records on the EA topic.
- **Format rule:** every artifact is a discrete file with a machine-checkable name pattern (`adr-NNN-<slug>.md`, `spec-<capability>-components.md`) so the spooler and RAG can index it.

## Constraints & Permissions
- Read: RAG knowledge base, Git repo, platform standards.
- Write: architecture artifacts into the Git repo; work packages onto the EA topic.
- No direct production code writes — implementation goes through the Solution Architect and engineering channels.
- Never invent platform standards locally; when RAG has no answer, flag the gap and escalate rather than guess.

## Fallback Procedures
- **RAG miss on a standard:** state the assumption explicitly in the ADR, mark it "provisional," and route the gap to the Business Org / principal for ratification.
- **Spooled worker returns garbage or no artifact:** reject with a specific defect list, re-spawn with the corrected work package, max 2 retries, then escalate.
- **Requirements conflict undecidable here:** emit the conflict matrix and route to the Business Org through the PM/RA channels — do not silently resolve it.
- **Tooling outage (topic/spooler down):** park artifacts in the Git repo and log the delegation intent so it can be replayed when the bus recovers.
