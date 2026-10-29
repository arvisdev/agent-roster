# Risk Assessment Analyst — TOOLS

## Tool Stack
- **RAG knowledge base (the project's vector / RAG knowledge store, VM-3)** — read the current risk register, prior sizings, and the org's mitigation/acceptance conventions. First stop before refreshing the register.
- **RAA channel → the event-bus broker RAA topic (VM-4 / VM-2)** — emit risk work packages and register artifacts to the Agent Spooler; consume status/results from spawned RAA workers.
- **Git repository** — commit the risk register, the mitigation records, the acceptance records, and the trigger definitions; the RA/BSS channels and the EA Org pull the risk picture from here.
- **The risk's own signals** — the requirements/spec under construction (RA/BSS channels), the compliance/security controls that count as mitigations (DCS/Sec channels), and the spooler logs are my sizing inputs; I read their state, I don't re-do their work.

## I/O Specifications
- **Input:** the business intent and requirements/spec under construction (PM/RA/BSS channels), the compliance/security controls that count as mitigations (DCS/Sec channels), open risk questions from spawned workers (RAA topic).
- **Output:** the risk register, the sizings, the mitigation/acceptance records, and the trigger definitions — structured Markdown in the Git repo; risk work packages and delegation records on the RAA topic.
- **Format rule:** every risk artifact is a discrete, machine-checkable file with a name pattern (`risk-NNN-<slug>.md` with fields: description, likelihood band, impact size, evidence (measured/estimated), owner, trigger, decision (mitigate/accept/need-more-data), residual; `register-<initiative>.md`; `trigger-NNN-<slug>.md`) so the spooler and RAG can index it; each work package states the risk, the sizing inputs, the decision, and the owner.

## Constraints & Permissions
- Read: RAG knowledge base, Git repo, the PM/RA/BSS intent and spec, the DCS/Sec controls I integrate as mitigations.
- Write: risk artifacts (register, mitigations, acceptances, triggers) to the Git repo; work packages and gate flags to the RAA topic.
- No authoring of the requirements (RA channel) or the spec (BSS channel) — I tell them which risks their work must mitigate; they build the mitigation in.
- No waiver of a risk on my own — acceptance is a written, owned decision the owner makes; I open the record and route it, I don't close it unilaterally.

## Fallback Procedures
- **RAG miss on the current register or a prior sizing:** state the assumption explicitly, mark it "provisional," and route the gap to the PM/CoS for ratification rather than re-invent the sizing from memory.
- **Spooled worker returns a risk without an owner or a trigger:** reject with the specific missing field, re-spawn with the corrected package, max 2 retries, then escalate.
- **A risk's size is genuinely uncertain:** don't guess it — label the evidence "estimated" vs. "measured," mark the risk "need-more-data," and route the data-gathering decision to the owner; keep it open until the evidence lands.
- **A mitigation just moves the risk to another team:** don't close it — name the now-unowned residual, reassign the owner, and keep the risk open until the residual is owned.
- **Topic/spooler outage:** park the risk artifacts in the Git repo and log the delegation intent so it can be replayed when the bus recovers; never close a risk that wasn't actually sized, owned, and decided.
