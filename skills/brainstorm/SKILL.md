---
name: brainstorming
description: Use before implementation when a feature or behavior change has unresolved product intent, scope, architecture, or meaningful implementation tradeoffs. Explore the relevant project context, clarify uncertainty, compare viable approaches, and get approval for a proportionate design. Skip for explicit low-risk changes whose intended outcome and implementation are already clear.
---

# Brainstorming

Turn an uncertain idea into an approved, implementation-ready design through focused discussion.

## Decide Whether Brainstorming Is Needed

Use this workflow when implementation depends on a product decision, unclear requirement, uncertain scope, architectural choice, or meaningful tradeoff.

Do not add a design round when the user has already given specific, low-risk instructions and the repository confirms how to implement them. Prior approval counts; never ask for redundant approval.

## Workflow

1. **Explore context** — inspect the relevant files, documentation, conventions, and recent changes until the current behavior and constraints are clear.
2. **Bound the problem** — state the goal, scope, constraints, and success criteria. If the request contains independent subsystems, decompose it before designing the first part.
3. **Resolve uncertainty** — ask only questions whose answers materially affect the design and cannot be verified from available context. Ask one at a time when each answer determines the next question; otherwise ask the smallest focused set.
4. **Compare viable approaches** — when multiple credible approaches exist, explain their meaningful tradeoffs and recommend one. Do not invent alternatives to satisfy a quota.
5. **Present the design** — describe the proposed behavior, boundaries, implementation direction, and validation strategy in chat. Include architecture, data flow, error handling, migration, or testing only when relevant.
6. **Get approval** — request one approval for the complete design before implementation. If the user changes the design, revise it and request approval again.
7. **Record when warranted** — write a specification only when the user requests one or the work is complex enough to need a durable implementation reference. Ask where it should live before creating it.

The workflow is complete when the remaining implementation decisions can be made from repository evidence and the user has approved every material product or architectural choice.

## Design Guidance

- Scale the design to the risk and complexity of the change. A small decision may need one paragraph; a cross-cutting feature may need several sections.
- Follow existing repository patterns unless changing them directly serves the requested outcome.
- Prefer clear boundaries and independently testable behavior, but do not introduce abstractions without a concrete need.
- Include targeted cleanup when existing problems obstruct the change. Exclude unrelated refactoring.
- Remove speculative requirements and features that are not needed for the stated success criteria.

## Specification Review

When a written specification is warranted, review it before presenting it:

- Remove placeholders and incomplete sections.
- Resolve contradictions between requirements and the proposed design.
- Confirm the scope fits one implementation effort; decompose it if it does not.
- Make repository-verifiable details explicit.
- Ask the user about unresolved product decisions instead of choosing silently.

Do not commit the specification unless the user explicitly asks.

## Transition

After approval, continue according to the user's requested workflow. Write an implementation plan only when requested or when the remaining work is complex enough that a plan materially improves execution.
