---
name: self-review
description: Review finished work before handoff for codebase rule compliance, missing implementation, overengineering, and tests that lack meaningful behavioral coverage. Use when asked to self-review or audit a completed change.
---

# Self-review

Review the actual result against the agreed task and the codebase's rules. Prioritize broken requirements and rule violations over stylistic preferences. Review alone authorizes inspection and checks; make fixes only within existing user authorization.

## 1. Establish the review scope

Read the original request, accepted decisions, and acceptance criteria. For ticket-driven work, reread the ticket. Inspect the current diff, relevant new files, and affected consumers. Use the requested baseline; distinguish the completed work from unrelated local changes. Ask only if the scope cannot be resolved from available evidence.

Complete this step when every changed file is accounted for and each requirement has an implementation location or an identified gap. Keep this mapping in working notes; surface only findings and unresolved items.

## 2. Check codebase rules first

Discover applicable instructions from the repository root through each changed path, including AGENTS.md, CLAUDE.md, contributing guides, and documents they require. Inspect package scripts, toolchain settings, lint and format configuration, and relevant CI jobs. Read nearby code and tests to establish conventions where written guidance is absent.

For each applicable rule, record evidence of compliance, a violation, a justified exception under the instruction hierarchy, or an unverified status. Distinguish explicit requirements from inferred conventions. Verify rules against the actual files and command results rather than the implementation's summary.

Check especially:

- Scope boundaries, required workflows, and prescribed validation.
- Module boundaries, API contracts, error handling, and existing consumers.
- Types, naming, dependencies, comments, documentation, and generated files.
- Package manager, toolchain, formatting, and testing conventions.

Complete this step when every discovered applicable rule has a status. Missing access or an unavailable check remains a reported gap; it does not count as compliance.

## 3. Review completeness and complexity

Trace each requirement through the changed code to its observable result. Inspect integration points and affected callers for unwired paths, omitted branches, incomplete error handling, and placeholders. A passing isolated test does not establish that the feature is connected to its consumers.

For each added abstraction, dependency, configuration option, fallback, and compatibility layer, identify the current requirement or existing consumer that justifies it. Flag complexity that serves only hypothetical future use, duplicates existing facilities, or can be replaced with a simpler implementation that meets the same requirements.

Evaluate defensive checks against real runtime boundaries and enforced types. Preserve complexity required by supported consumers, reliability, security, or repository conventions. Prefer the smallest correction that fixes the demonstrated problem.

Complete this step when all requirements have been traced and each complexity finding names both the unnecessary cost and a concrete simpler alternative.

## 4. Review test value

Inspect each added or changed test and relevant existing coverage. Identify the behavior it protects, the realistic regression it would catch, and whether its assertions distinguish correct behavior from that regression.

Flag tests whose only result is repeating constants or configuration, reproducing the implementation's calculation, asserting internal call sequences without a contract, or checking mocks instead of production behavior. Also flag redundant cases that protect the same behavior without exercising a distinct risk.

Keep constant, configuration, snapshot, and interaction assertions when they verify a real external contract or meaningful behavior. Explain the missing value before recommending removal; classify tests by what they prove, not by their syntax.

Identify missing coverage for changed behavior and plausible failure paths. Suggest tests only where they would catch a meaningful regression. When a test's value is unclear, reason through a concrete faulty implementation or use a small reversible mutation if warranted; ensure any temporary edits are restored.

Complete this step when each changed test has an identified purpose or finding, and meaningful coverage gaps are recorded.

## 5. Verify and report

Run the repository-required checks and focused validation for the changed behavior using its prescribed tools. Reuse recent results only when they cover the current files and revision. Broaden validation when the affected scope or a failure warrants it. Report blocked or skipped checks with their reason.

List actionable findings concisely, ordered by impact. Use simple, easy-to-understand ASD-STE100 Simplified Technical English: short sentences, direct verbs, and one point per sentence. Explain necessary technical terms. Each finding must include a file and line where available, the violated rule or requirement, the concrete consequence, and the smallest recommended correction. Separate confirmed issues from unresolved questions and verification gaps. Keep unsupported style preferences out of the findings.

If fixes are authorized, apply the relevant corrections, rerun affected checks, and review the final diff again. Preserve unrelated work and stay within the agreed scope.

Finish when all review steps have evidence and all findings are either corrected and verified or clearly reported. If no actionable issues remain, state that briefly with the checks performed and any verification limits. Claim full rule compliance only when every applicable rule has been verified.
