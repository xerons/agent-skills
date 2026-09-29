---
name: dev-doctor
description: Use when the user asks to audit or diagnose a repository's AI-assisted development setup, including agent instructions, skill references, and tool prerequisites.
---

# Dev Doctor

Audit the current repository's AI development setup using local evidence. The default audit is read-only. This skill checks whether the setup is understandable and usable; it does not diagnose application bugs or bootstrap a new project.

## Inspect the setup

1. Identify the user-requested workflow or host when specified. Inspect applicable `AGENTS.md`, `CLAUDE.md`, or equivalent agent instructions, plus the setup files they refer to.
2. Check only relevant skill and tool references. Verify skill names against the current runtime's available skill inventory and paths against the filesystem. Verify tool availability from the current tool inventory or an appropriate local check. Say when a reference is not checked or is unavailable in this session; do not claim it is globally absent based on this session alone.
3. Look for direct evidence of broken, contradictory, stale, missing, or unclear instructions. Treat a file or convention being absent as a finding only when the project's stated workflow depends on it. Do not prescribe a generic template just because the repo lacks one.
4. Separate observed facts from interpretation. Include paths or the relevant tool result for each finding. If information needed for a meaningful conclusion is unavailable, state that limit or ask one short question.

## Classify findings with Jev

For a set of evidence-backed findings, consult the `typesafe-ai` skill and use Jev's `mcp__jev__jev_classify` (or the equivalent Jev classification tool available in the host) to assign one of these priorities:

- **Blocking** — the user-requested development workflow cannot run because a required setup element is broken or unavailable.
- **Attention** — conflicting or stale setup is likely to cause the wrong workflow or avoidable friction.
- **Advisory** — a supported improvement that is optional for the stated workflow.
- **Needs investigation** — available evidence is insufficient to assign impact.

Provide Jev with concise findings and their evidence, the requested workflow, and these class definitions. Treat Jev's result as a prioritization judgment, not proof that a file or tool exists. The primary reasoning agent verifies the evidence and handles open-ended interpretation. If Jev flags uncertainty, review the evidence and mark the finding as needing investigation when it remains unclear. If Jev is unavailable, classify with the primary reasoning agent and disclose that fallback.

Do not give the repository an arbitrary numeric health score. A missing file is not automatically a blocker.

## Keep the audit read-only

- Do not edit repository files, install tools or skills, or fetch remote resources during an audit unless the user explicitly asks for that action.
- When the user asks for fixes, make only clear, local, reversible changes within the requested scope. Ask about unresolved project choices; do not silently choose a policy.
- Do not diagnose product bugs, review general code quality, or run broad project builds/tests as part of this setup audit. Hand those requests to an appropriate workflow.
- Do not duplicate project bootstrapping. If the user wants to add missing setup to a new repo, use `dev-setup` when available.

## Report

Give a short summary, then list actionable findings in priority order. For each finding include its priority, evidence, impact on the requested workflow, and a proposed next step. Keep optional suggestions separate from faults. If fixes were requested and made, list the exact files changed and checks actually run. State what could not be inspected; do not claim a clean bill of health beyond the inspected scope.
