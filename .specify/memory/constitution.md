<!--
Sync Impact Report

- Version change: none → 1.0.0 (initial ratification)
- Modified principles:
  - P1: Library-First Architecture
  - P2: CLI-First Text Interfaces
  - P3: Test-First Delivery
  - P4: Integration & Flow Testing
  - P5: Observability, Versioning & Simplicity
- Added sections: none (all sections were present as template placeholders)
- Templates reviewed:
  - .specify/templates/plan-template.md ✅ updated (Constitution Check gates now reference principles)
  - .specify/templates/spec-template.md ✅ aligned with principles (independent, testable user stories)
  - .specify/templates/tasks-template.md ✅ aligned with principles (story-grouped tasks, tests and cross-cutting concerns)
- Command templates: ⚠ pending (no `.specify/templates/commands` directory in this repo)
- Deferred TODOs: none (all placeholders resolved; future amendments require version bump)
-->

# Cline Project Constitution

## Core Principles

### Library-First Architecture

Every new capability is designed as a small, focused unit of logic that can be reasoned
about and tested in isolation. Where possible, functionality is extracted into
reusable libraries or modules rather than embedded directly into ad-hoc scripts or
tools.

- Libraries MUST be self-contained and independently testable.
- Each library or module MUST have a clear, documented purpose.
- Shared code MUST live in libraries, not copied across commands or workflows.
- Feature-specific wiring (CLI, UX, orchestration) MUST remain thin and delegate to
  these libraries.

Rationale: A library-first approach keeps the codebase maintainable, encourages reuse,
and makes it easier to test and reason about behavior as the project grows.

### CLI-First Text Interfaces

All automation and workflows MUST be accessible via command-line interfaces with
deterministic text-based input and output. This applies to both human-triggered
commands and automated processes.

- Commands MUST accept configuration via arguments, environment variables, and/or
  stdin.
- Normal results MUST be written to stdout; errors MUST be written to stderr with
  actionable messages.
- Where structured data is required, commands SHOULD support JSON in addition to
  human-readable text.
- Commands MUST avoid interactive prompts by default so they can run non-interactively
  in CI and automation.

Rationale: CLI-first, text-based interfaces make behaviors transparent, scriptable,
and easy to integrate into diverse environments, including editors, CI pipelines, and
external tools.

### Test-First Delivery

Changes MUST be driven by clearly defined behavior and tests.

- Each feature MUST be anchored in independently testable user stories defined in the
  spec (`spec-template.md`).
- For each user story, an independent test strategy (acceptance scenarios, automated
  tests, or both) MUST be described before implementation begins.
- Where automated tests are in scope, tests SHOULD be written before or alongside the
  code, and verified to fail before implementation is considered complete.
- Regressions discovered in production or manual testing MUST result in new or
  updated tests that would have caught the issue.

Rationale: Test-first delivery reduces regressions, documents intent, and ensures that
changes solve real, verifiable problems instead of drifting from user needs.

### Integration & Flow Testing

Unit tests alone are insufficient. The system MUST be validated end-to-end along the
same flows that users and tools actually execute.

- Critical paths (e.g., from spec → plan → tasks → implementation) MUST be
  demonstrably executable without manual patching of intermediate artifacts.
- When contracts, interfaces, or workflows change, corresponding integration or flow
  tests MUST be updated.
- Any new cross-module behavior (e.g., multiple libraries collaborating) MUST be
  covered by at least one integration or flow-level test.
- Breaking changes to interfaces MUST be accompanied by migration notes and, where
  feasible, temporary compatibility shims.

Rationale: Integration and flow testing catches mismatches between components and
ensures that the documented workflow is actually executable in practice.

### Observability, Versioning & Simplicity

The system MUST be observable, evolve predictably, and remain as simple as possible
while meeting real needs.

- Logging MUST be structured enough to correlate user actions, commands, and errors.
- Error messages MUST clearly communicate what failed and how to act on it.
- Public behaviors (CLI flags, file formats, protocol contracts) MUST be treated as
  versioned interfaces.
- Backwards-incompatible changes to public behaviors MUST be paired with a
  documented migration path and an appropriate version bump.
- Designs MUST favor the simplest approach that satisfies the requirement; additional
  layers of abstraction require explicit justification.

Rationale: Good observability and disciplined versioning make the system debuggable
and change-tolerant. Simplicity keeps onboarding and maintenance costs under control.

## Additional Constraints & Safety Requirements

This project prioritizes safety, clarity, and incremental delivery.

- Potentially destructive operations (file system changes, external API calls,
  deployments) MUST be explicit and require human review or opt-in configuration.
- Automated commands MUST default to the safest behavior; irreversible operations
  MUST be clearly documented and, where possible, reversible.
- Each phase of work (specification, planning, tasks, implementation) MUST resolve
  known issues before moving to the next phase; known violations MUST be documented
  with rationale.
- Repository-specific rules (for example, how to communicate changes to the end
  user) MUST be honored in both code and documentation.
- External integrations (MCP servers, tools, services) MUST be documented with
  required configuration (keys, URLs, permissions) and failure modes.

Rationale: Strong constraints around safety and clarity reduce the risk of accidental
data loss or misconfiguration and make the development process predictable.

## Development Workflow & Quality Gates

The development workflow is organized around the `/speckit.*` commands and the
artifacts they manage.

- New work starts with a feature specification that defines independently testable
  user stories, edge cases, and success criteria.
- An implementation plan MUST be created that selects an appropriate project
  structure and records technical context and constraints.
- A task list MUST then be generated, grouped by user story, with clear file paths
  and dependencies.
- Implementation MUST follow the plan and tasks; deviations MUST be documented and,
  when material, reflected back into the spec/plan/tasks.

Quality gates:

- **Constitution Check** in the plan MUST be passed before starting deep design or
  implementation. This includes verifying that:
  - User stories are independently testable and prioritized.
  - Technical context is sufficiently detailed to support implementation decisions.
  - Safety constraints and external dependencies are identified.
- Before merging, changes MUST:
  - Keep spec, plan, and tasks consistent with the implemented behavior.
  - Either add or update tests (where in scope) or explicitly justify why tests are
    not added.
  - Document any breaking changes and their migration path.

Rationale: A structured workflow with clear gates ensures that work is always grounded
in user value, technically feasible, and verifiable.

## Governance

This constitution defines the non-negotiable rules for how this project is evolved
and maintained.

- The constitution supersedes informal habits and prior undocumented practices.
- Any substantial change to principles, governance rules, or workflow MUST be made
  via a documented change (for example, a pull request) that updates this file and,
  where relevant, the associated templates.
- Each amendment MUST specify the new version number, amendment date, and a brief
  rationale for the change.
- Versioning of the constitution follows semantic versioning:
  - MAJOR: Backwards-incompatible governance or principle changes.
  - MINOR: New principles/sections or materially expanded guidance.
  - PATCH: Clarifications, wording, and non-semantic refinements.
- Compliance expectations:
  - Reviews MUST include a check for adherence to this constitution.
  - Deviations MUST be explicitly called out, justified, and, if recurring, resolved
    via an amendment rather than one-off exceptions.
  - Tooling (including `/speckit.*` commands) SHOULD evolve over time to automate as
    many of these checks as practical.

**Version**: 1.0.0 | **Ratified**: 2026-01-22 | **Last Amended**: 2026-01-22
