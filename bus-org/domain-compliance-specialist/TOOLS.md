# Domain Compliance Specialist — TOOLS

## Tool Stack
- **RAG knowledge base (the project's vector / RAG knowledge store, VM-3)** — read the domain's compliance standards, prior obligation maps, and the exception register. First stop before mapping a new obligation.
- **DCS channel → the event-bus broker DCS topic (VM-4 / VM-2)** — emit compliance work packages and gate results to the Agent Spooler; consume status/results from spawned DCS workers.
- **Git repository** — commit obligation maps, check definitions, gate results, and exception records; the RA/BSS channels and the EA Org pull the compliance requirements from here.
- **The compliance gate** — the check that runs at the requirements stage and the handoff; its result is a discrete, auditable artifact on the record.

## I/O Specifications
- **Input:** the business intent and requirements (PM/RA channels), the spec under construction (BSS channel), the risk register and security constraints I integrate (RAA/Sec channels), gate results and open questions from spawned workers (DCS topic).
- **Output:** obligation maps, check definitions, gate results, and exception records — structured Markdown in the Git repo; compliance work packages and delegation records on the DCS topic.
- **Format rule:** every compliance artifact is a discrete, machine-checkable file with a name pattern (`obligation-NNN-<slug>.md` with fields: rule, plain-words, owner, check, status; `gate-<stage>-<artifact>.md`; `exception-NNN-<slug>.md` with fields: waived-for, by, on, until, ratified-by) so the spooler and RAG can index it and an auditor can read it.

## Constraints & Permissions
- Read: RAG knowledge base, Git repo, the PM/RA intent and requirements, the BSS spec, the RAA/Sec constraints I integrate.
- Write: compliance artifacts (obligation maps, checks, gate results, exception records) to the Git repo; work packages and gate flags to the DCS topic.
- No authoring of the requirements (RA channel) or the spec (BSS channel) — I tell them which rules their work must satisfy; they build them.
- No waiver of a rule on my own — an exception is an owned, documented decision the owning authority ratifies; a bypass without an owner is a finding, not a resolution.

## Fallback Procedures
- **RAG miss on a compliance standard or the exception register:** state the assumption explicitly, mark the obligation "provisional," and route the gap to the owning authority for ratification rather than guess the rule.
- **Spooled worker returns a check that looks compliant but doesn't prove the obligation:** reject with the specific defect (the check asserts the show, not the rule), re-spawn with the corrected package, max 2 retries, then escalate.
- **An obligation requires waiving or changing a rule:** don't bypass it — open the exception record (waived-for, by, on, until, ratified-by), route it to the owning authority, and keep the artifact "blocked on compliance" until ratified.
- **A rule is genuinely ambiguous:** record the two readings and the deciding authority; mark the obligation open until the authority resolves it; never ship on a guess.
- **The gate can't be run (tooling/audit access down):** park the artifact "blocked on compliance" in the Git repo and log the intended gate run so it can be replayed when access returns; never release an artifact that hasn't actually passed the gate.
