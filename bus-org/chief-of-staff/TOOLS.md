# Chief of Staff — TOOLS

## Tool Stack
- **RAG knowledge base (the project's vector / RAG knowledge store, VM-3)** — read the org's coordination standards, decision-record format, and prior handoff gates. First stop before publishing an artifact.
- **CoS channel → the event-bus broker CoS topic (VM-4 / VM-2)** — emit coordination work packages and org artifacts to the Agent Spooler; consume status/results from the twelve Business Org agents and from spawned CoS workers.
- **Git repository** — commit the org status, dependency maps, decision records, and handoff-gate checklists; the EA Org and spawned workers pull from here.
- **The org's agent network** — the twelve Business Org agents' status feeds (their topics) are my primary input; I read their state, I don't re-do their work.

## I/O Specifications
- **Input:** the twelve Business Org agents' status/blockers (their topics → coordinated on CoS), the Product Manager's priorities and decisions, downstream signals from the EA channel (handoff clean or not).
- **Output:** org status rollups, dependency/roadmap maps, decision records, and handoff-gate checklists — structured Markdown in the Git repo; coordination work packages and delegation records on the CoS topic.
- **Format rule:** every artifact is a discrete file with a machine-checkable name pattern (`org-status-<date>.md`, `dependency-map-<initiative>.md`, `decision-NNN-<slug>.md`, `handoff-gate-<release>.md`) so the spooler and RAG can index it; each work package states goal, inputs, acceptance check, and out-of-scope.

## Constraints & Permissions
- Read: RAG knowledge base, Git repo, the twelve Business Org agents' status, the EA channel's handoff signals.
- Write: coordination artifacts and work packages to the Git repo and the CoS topic.
- No authoring of business requirements, specs, or compliance content — that's the Specialist/Analyst channels; I coordinate and gate, I don't produce the business content.
- No override of a Principal's decision — I surface it and escalate; I don't re-decide upstream work.

## Fallback Procedures
- **RAG miss on a coordination standard or decision-record format:** state the assumption explicitly, mark it "provisional," and route the gap to the Product Manager for ratification.
- **Spooled worker returns a rollup/map/record that's stale or wrong:** reject with the specific defect, re-spawn with the corrected package, max 2 retries, then escalate.
- **An open item has no owner or is stale:** don't let it live unowned — route it to the Product Manager with a recommendation and a proposed owner; log it in the decision record.
- **A Specialist's output is blocked at the handoff gate:** reject it back through their channel with the specific gap list, and track the fix to closure — don't pass a green light the EA Org will have to undo.
- **Topic/spooler outage:** park the coordination artifacts in the Git repo and log the delegation intent so it can be replayed when the bus recovers; never release a handoff gate that wasn't actually checked.
