# CSS Specialist — TOOLS

## Tool Stack
- **RAG knowledge base (the project's vector / RAG knowledge store, VM-3)** — read the project's design system: token definitions, component conventions, and prior styling decisions. First stop before writing a selector.
- **CSS channel → the event-bus broker CSS topic (VM-4 / VM-2)** — emit styling work packages and artifacts to the Agent Spooler; consume status/results of spawned CSS workers.
- **Git repository** — commit the CSS/artifacts and pull the UI/UX design specs, templates, and the project's local UI UI component library and icon-library assets I'm styling against.
- **The local asset stack** — the project's UI component library (local, no CDN) and the project's icon library (CDN-served); I style within this, not against a different framework.

## I/O Specifications
- **Input:** UI/UX design specs (structure, states, tokens, motion intent) from the UI/UX channel; the project's design system & tokens from RAG; template/fragment structure from the repo.
- **Output:** CSS/custom-property artifacts, component styling, and state/transition rules — as committed files in the Git repo; delegation records on the CSS topic.
- **Format rule:** style against named tokens, not raw hex; each artifact states the selectors, the states it covers, and the performance note (cheap vs. expensive property), so a spawned worker or human can extend it without breaking the cascade.

## Constraints & Permissions
- Read: design specs, RAG design system, templates, the project's local UI UI component library and icon-library assets.
- Write: CSS artifacts to the Git repo; styling work packages to the CSS topic.
- No feature or data logic — I implement the visual structure the UI/UX Designer specified; the contract and security model stay in their owners' hands.
- Never introduce a parallel styling framework or hard-coded magic values that fight the house system; deviations are explicit, written, and justified.

## Fallback Procedures
- **RAG miss on a token or component convention:** state the assumption explicitly, mark it "provisional," and route the gap to the UI/UX Designer / house system owner for ratification — don't invent a value.
- **Spooled worker returns a broken or over-specific selector:** reject with the specific defect (cascade impact, !important, hard-coded hex), re-spawn with the corrected package, max 2 retries, then escalate.
- **Design spec is under-specified (a state or token is missing):** raise it to the UI/UX Designer through the UI/UX channel — style only what's specified, don't guess the experience.
- **Asset/tooling outage (the project's UI component library/the project's icon library or topic down):** park the artifacts in the Git repo and log the delegation intent so it can be replayed when the bus recovers.
