---
name: dev-discovery
description: Use to clarify a software idea or design through interactive decision rounds and prepare a pre-implementation handoff; dev-coach also uses it as its discovery step.
---

# Dev Discovery

Run the discovery phase independently or as the first step of `dev-coach`. Use the Ask Matt routing distinctions to select a discovery path, resolve decisions with the user, preserve durable project knowledge, and stop with a clear handoff before source implementation.

## Choose the route

Honor a route the user names or an `ask-matt` recommendation already supplied in the conversation. Otherwise use these Ask Matt distinctions:

- **`grill-me`** for a bounded idea or design without a project workspace.
- **`grill-with-docs`** for a bounded design in an existing codebase, where decisions should be recorded in the project glossary or ADRs.
- **`wayfinder`** for a large, foggy effort that needs a multi-session decision map.

Do not use Jev to make the same route choice. Ask one short question only when the route remains unclear or none fits. The `ask-matt` entry point recommends a route and stops; this skill applies its routing distinctions and owns the discovery handoff. Do not claim that `ask-matt` or a user-invoked Matt skill ran unless the user invoked it.

For the two interview routes, use the model-invoked `grilling` skill for the design-tree interview. Use `domain-modeling` when a codebase route needs glossary or ADR work. `grill-me` leaves no project artifacts. `grill-with-docs` updates the project's glossary and records consequential decisions as ADRs, following its existing conventions.

`wayfinder` is an explicit user-invoked planning workflow with its own map and ticket process. If selected, tell the user that `/wayfinder` is the next command and stop at that handoff; resume discovery when the user returns with the map or asks to continue. Do not substitute a short grilling session for a Wayfinder map.

## Run the interview

Before asking, inspect the target project's `AGENTS.md`, code, terminology, and documentation. Resolve factual questions from the project first. Keep decisions with the user.

Present each round through Plannotator's browser interview when available. Use `plannotator-setup-goal` only to prepare its interview UI: keep the temporary bundle and result outside the project, run only the interview phase, and remove temporary files when the round is resolved. If Plannotator is unavailable, use a self-contained HTML form only when the host can return submitted answers to the conversation; otherwise ask a concise round in chat.

Show independent questions on the current decision frontier together. Keep dependent questions for later rounds. Include a recommended answer, useful choices, and a custom answer; preserve earlier answers in the same round for review. Read every answer and note, then resolve blocking uncertainty before opening the next round. Skip the interview when the request and project context already settle the decisions.

## Finish at the implementation boundary

Return a handoff with the goal, settled decisions, constraints, acceptance criteria, project terminology and ADRs updated, remaining uncertainty, and the next implementation step. Carry the handoff to `dev-coach` when it called this skill. Stop before editing source code; the caller decides whether to continue into specification, tickets, or implementation based on the user's request.

For a plan-only request, stop at the requested map or handoff. When Wayfinder owns the route, its explicit command is the handoff. For a request to ship, state whether the decisions are ready for implementation and name any remaining preparation, such as a spec or ticket breakdown, before the implementation skill begins.
