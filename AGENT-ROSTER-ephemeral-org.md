# AGENT ROSTER (ephemeral-org)

Ephemeral spooler workers — single-task, artifact-first agents spawned per work
package, do the assigned job, produce the artifact, and exit. Mirrors the bus-org
and ea-org archetypes in scoped, one-shot form.

Backend Engineer
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-backend-engineer
Description: Software Engineer that codes backend applications — implements service components, data-access layers, event producers/consumers, or fixes a specific backend defect — pick for scoped backend code work packages
Model: z-ai/glm-5.3-flash
Image: claude-code

Behavioral Specification Specialist
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-behavioral-specification-specialist
Description: Decomposes requirements into sub-behaviors, writes Gherkin specs and acceptance criteria, and links sub-behaviors to requirements — pick for formal behavioral specification artifacts
Model: z-ai/glm-5.3-flash
Image: hermes-agent

Business Requirements Specialist
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-business-requirements-specialist
Description: Business Analyst that specializes in building and gathering business requirements — structures requirements into BRS-NNN form, checks completeness, maintains traceability, and closes ambiguities — pick for business-requirement authoring and cleanup
Model: z-ai/glm-5.3-flash
Image: hermes-agent

Chief of Staff
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-chief-of-staff
Description: Compiles org status rollups, dependency/critical-path maps, decision records, and handoff-gate checklists — pick for coordination and cross-agent visibility artifacts
Model: z-ai/glm-5.3-flash
Image: hermes-agent

CSS Specialist
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-css-specialist
Description: Styles components against house tokens, completes hover/focus/transition states, fixes specificity and performance issues, and reviews styling drift — pick for scoped CSS work
Model: z-ai/glm-5.3-flash
Image: claude-code

Data Architect
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-data-architect
Description: Writes data-store schemas, migration scripts, event-bus message schemas, and QA-reviews data contracts — pick for data-contract and schema definition work
Model: z-ai/glm-5.3-flash
Image: claude-code

Data Engineer
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-data-engineer
Description: Implements idempotent data pipelines and transforms, writes data-quality checks, debugs and backfills failures, and authors runbooks — pick for pipeline execution work
Model: z-ai/glm-5.3-flash
Image: claude-code

Domain Compliance Specialist
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-domain-compliance-specialist
Description: Maps capabilities to named, owned obligations, writes met/not-met checks, compiles compliance gate results, and authors exception records — pick for regulatory/compliance gatekeeping
Model: z-ai/glm-5.3-flash
Image: hermes-agent

Domain SME
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-domain-sme
Description: Authors glossary entries, process models, decision rules, and edge-case notes, and reviews requirements against domain ground truth — pick for subject-matter expertise and domain validation
Model: z-ai/glm-5.3-flash
Image: hermes-agent

Enterprise Architect
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-enterprise-architect
Description: Drafts component and contract specs, ADRs, diffs designs against the platform reference architecture, and QA-reviews specs — pick for enterprise-level architecture documents and decisions
Model: z-ai/glm-5.3-flash
Image: hermes-agent

Full-Stack Engineer
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-fullstack-engineer
Description: Software Engineer that codes both backend and frontend applications — implements features end-to-end per integration/data contracts, writes server-rendered templates, and fixes cross-boundary integration defects — pick for full-stack feature work packages
Model: z-ai/glm-5.3-flash
Image: claude-code

Process Improvement Analyst
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-process-improvement-analyst
Description: Maps intent-to-build flows, measures baseline cycle time, rework, and wait at handoffs, compiles improvement cases, and documents proven practices — pick for process analysis and optimization
Model: z-ai/glm-5.3-flash
Image: hermes-agent

Product Manager
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-product-manager
Description: Writes intent statements, compiles prioritized backlogs, authors measurable outcome definitions, and maps intent-vs-constraint conflicts — pick for product intent and prioritization artifacts
Model: z-ai/glm-5.3-flash
Image: hermes-agent

Quality Assurance Specialist
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-quality-assurance-specialist
Description: Verifies sub-behaviors against observables, runs acceptance tests, curates evidence, builds release-gate checklists, and compiles gap reports — pick for QA verification and release gating
Model: z-ai/glm-5.3-flash
Image: hermes-agent

Requirements Analyst
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-requirements-analyst
Description: Structures requirement batches into identified, owned, testable form, maintains traceability, reviews ambiguity, and checks scope definitions — pick for requirements structuring (the business-facing variant is eph-business-requirements-specialist)
Model: z-ai/glm-5.3-flash
Image: hermes-agent

Risk Assessment Analyst
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-risk-assessment-analyst
Description: Maps failure modes into the risk register, sizes likelihood × impact, compiles mitigation and acceptance records, and defines risk triggers — pick for risk assessment and mitigation
Model: z-ai/glm-5.3-flash
Image: hermes-agent

Security Architect
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-security-architect
Description: Implements security controls, fixes secrets-handling defects, writes container hardening configs, and verifies findings with evidence — pick for hands-on security work packages
Model: z-ai/glm-5.3-flash
Image: claude-code

Solution Architect
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-solution-architect
Description: Produces module implementations and specs, schema/migration files, containerized deployment configs, and spec-gap analyses against the EA envelope — pick for concrete solution-design and deployment artifacts
Model: z-ai/glm-5.3-flash
Image: claude-code

Stakeholder Analyst
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-stakeholder-analyst
Description: Maps stakeholders on interest/power quadrants, traces positions to sources, records decision collisions, and recommends handling strategies — pick for stakeholder and conflict analysis
Model: z-ai/glm-5.3-flash
Image: hermes-agent

Technical Feasibility Specialist
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-technical-feasibility-specialist
Description: Runs minimal buildability spikes against the real stack, estimates cost and effort, identifies binding constraints, and issues feasibility verdicts with evidence — pick for go/no-go feasibility calls
Model: z-ai/glm-5.3-flash
Image: hermes-agent

UI/UX Designer
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-uiux-designer
Description: Writes design specs, produces state and flow diagrams, checks accessibility, and reviews surfaces for design-system drift — pick for UI/UX design artifacts
Model: z-ai/glm-5.3-flash
Image: hermes-agent

Unit Test Engineer
Agent: https://github.com/arvisdev/agent-roster/tree/main/ephemeral-org/eph-unit-test-engineer
Description: Writes red-first deterministic tests for specific seams, hardens flaky tests at the root, reports coverage gaps, and sets up test harnesses — pick for scoped unit-test work
Model: z-ai/glm-5.3-flash
Image: claude-code
