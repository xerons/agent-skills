---
name: code-simplify
description: Use when the user explicitly invokes `$code-simplify` for a focused cleanup of recently changed or user-named code, reducing complexity while preserving behavior.
disable-model-invocation: true
---

# Code Simplify

Make code easier to read and maintain without changing what it does. Work on the current change or the target the user names. Do not broaden a focused cleanup into an unrelated refactor.

## Workflow

1. **Set the scope.** Use the current diff or recently changed files when they identify the target. Otherwise use the file or area the user named. If the target is unclear, ask one short question. Do not sweep the repository by default.
2. **Learn the local style.** Read applicable `AGENTS.md` instructions and nearby code. Follow the project's conventions and existing architecture; do not impose language, framework, or vendor-specific style rules.
3. **Find a real clarity win.** Look for unnecessary nesting, duplication, indirection, or unclear names. Prefer explicit, familiar code over compactness. Keep abstractions that make responsibilities or behavior easier to understand. If nothing would become meaningfully clearer, leave the code unchanged and say why.
4. **Make the smallest useful change.** Keep the diff within scope. Treat bug fixes and behavior changes as separate work: describe what you found and ask before expanding into them.
5. **Review and report.** Inspect the final diff for unrelated edits and behavior changes. Report what changed, why it is clearer, and which checks actually ran. Do not claim behavior is unchanged based on intent alone; distinguish code inspection from test or build evidence.

## Preserve behavior

- Preserve APIs, observable outputs, serialized formats, and existing control-flow outcomes.
- Do not rewrite string literals as part of simplification. This includes user-facing text, logs, errors, prompts, and data values.
- Do not change configuration, schemas, or contracts to make the code look simpler. If a worthwhile simplification depends on such a change, explain the tradeoff and get the user's direction first.
- Do not add features, fix unrelated bugs, remove useful abstractions, or optimize for fewer lines.
- Follow the user's and project instructions for verification. Never invent or claim checks that were not run.

When used as part of `$dev-coach`, run this only if the user asks for a simplification pass. Complete it before the teach-back so the explanation describes the final code.
