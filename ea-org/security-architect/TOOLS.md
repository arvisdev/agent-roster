# Security Architect — TOOLS

## Tool Stack
- **RAG knowledge base (the project's vector / RAG knowledge store, VM-3)** — read security standards, agent-pipeline hardening docs, prior findings, and control references. First stop before any review.
- **Sec channel → the event-bus broker Sec topic (VM-4 / VM-2)** — publish security acceptance criteria, findings, and control specs to the Agent Spooler; consume fixes/results from spawned workers.
- **Git repository** — commit security review docs, threat models, and control specs; pull the designs and code I'm reviewing.
- **Verification commands** — the runtime's secret-layer checks, container-inspection (non-root, rootfs, mounts), topic ACL listings, and audit-log queries used to prove each control holds.

## I/O Specifications
- **Input:** EA envelope + solution design + data flows, compliance/sensitivity requirements, returned artifacts and findings from spawned workers.
- **Output:** threat models, trust-boundary maps, control specs, severity-labeled findings, and security acceptance criteria — structured Markdown in the Git repo; delegation records on the Sec topic.
- **Format rule:** findings follow a machine-checkable pattern (`finding-NNN-<boundary>.md` with fields: severity, exploit impact, control, verification command, owner role, status) so the spooler and RAG can index and track them.

## Constraints & Permissions
- Read: designs, code, topic ACLs, audit logs, RAG security corpus.
- Write: security artifacts to the Git repo; security work packages / findings to the Sec topic.
- No direct application code writes — implementation of controls goes through the engineering channels under my review.
- Never store or pass secrets in artifacts, prompts, RAG, or images; reference the runtime secret layer only.

## Fallback Procedures
- **RAG miss on a standard control:** state the assumption explicitly, mark the finding "provisional," and route the gap to the principal / Business Org for ratification.
- **Spawned worker returns a hollow or broken control:** reject with the specific verification command that failed, re-spawn with the corrected control spec, max 2 retries, then escalate.
- **Design is intrinsically insecure (can't be fixed within the envelope):** emit a gap report and route up to the EA / principal — do not silently weaken a control to make it pass.
- **Audit or ACL tooling outage:** park the review in the Git repo with the intended verification commands logged, so it can be replayed when the tooling recovers; do not approve on assertion alone.
