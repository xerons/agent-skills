---
name: repo-map
description: Use when the user asks to understand or navigate a repository, its architecture, key code paths, conventions, or where a change belongs.
---

# Repo Map

Build a compact, evidence-backed orientation to the current repository or the specific area the user names. Keep the work read-only unless the user asks for a saved document or another concrete change.

## Explore the repository

1. **Set the scope.** If the user names a feature, subsystem, or intended change, map that area first. For a general orientation, inspect the repository overview, root structure, project manifests, and applicable agent instructions. Ask one short question only if the requested scope is too broad to make a useful map.
2. **Find the real entry points.** Follow manifests, executable entry points, registrations, routes, dependency injection, and references into the relevant modules. Read source code and docs before describing a flow; directory names alone are not evidence of behavior.
3. **Filter large candidate sets.** When there are many plausible files for a focused question, consult `typesafe-ai` and use Jev's `mcp__jev__jev_find` (or the equivalent Jev search tool in the host) to rank a bounded set of file summaries. Open the selected files and verify the flow yourself. If Jev is unavailable, filter with code search and disclose that fallback when it affects the result.
4. **Trace only useful detail.** Follow the primary control or data flow far enough to explain the roles of the main components, their important boundaries, and where state or external systems enter. Include commands only when they are present in project docs/manifests or confirmed by tool output.
5. **Separate facts from interpretation.** Link claims to relevant file paths and symbols, with line references when useful. Mark uncertain or uninspected areas rather than implying the whole repository was covered.

## Present the map

Use only the sections that answer the user's request. A general orientation usually needs:

- **Purpose:** what the repository appears to build, grounded in its own docs and code.
- **Structure:** the main directories or modules and their roles.
- **Key flow:** a short sequence showing how an important request, event, or data set moves through the code.
- **Where to start:** the likely files or symbols for the user's next task.
- **Useful commands:** verified run, build, or validation commands when available.

Keep the explanation compact and readable. Avoid a file-by-file dump, speculative architecture diagrams, arbitrary health scores, and long documents by default. Save the map or create diagrams only when the user asks. Do not debug defects, review overall code quality, or change code as part of orientation; hand those requests to the appropriate workflow.
