---
name: dev-coach
description: Use when the user explicitly invokes `$dev-coach` for end-to-end development help.
disable-model-invocation: true
---

# Dev Coach

Use this workflow only when the user explicitly invokes `$dev-coach`. It is an end-to-end development guide: clarify the work, choose the right existing workflow, help implement it, and finish with a Plannotator teach-back when implementation is complete. The teach-back is agent-led; do not quiz the user or require them to explain the code back.

## 1. Route the work with TypeSafe

Honor a route the user explicitly names. Otherwise consult the `typesafe-ai` skill and use Jev's bounded decision tool (`mcp__jev__jev_decide`, or the equivalent Jev decision tool exposed by the host) to choose one primary route from:

- **`grill-me`** for a focused, bounded design or implementation that needs clarification but not a durable spec or multi-session map.
- **`grill-with-docs`** when the work needs a durable design/spec discussion and project glossary or ADR updates.
- **`wayfinder`** when the destination is too large for one agent session and needs a staged decision map.

Give Jev the user's request, settled preferences from this conversation, relevant project facts, the route definitions, and any availability constraints. Include `ask_user`, `investigate`, and `none` as escape hatches. Preserve explicit user directions as the highest priority. Use Jev for this route selection and other bounded classification, filtering, or routing judgments; use Codex for architecture, open-ended reasoning, implementation, and explanations. Jev's recommendation does not establish facts or grant permission.

If Jev returns `ask_user`, or its distribution does not clearly favor one route, ask one short question in chat (use a terminal prompt only when an interactive terminal is available). If Jev returns `investigate`, inspect the missing project fact first. If Jev returns `none`, do not force a route: explain that no listed workflow fits and ask one short question about how to proceed. Do not open Plannotator just to resolve route uncertainty. If no Jev tool is available, choose the route with Codex and disclose that Jev was unavailable. Do not install missing skills without the user's request; explain the gap and use an available equivalent if the user wants to continue.

Tell the user briefly which route was chosen and whether Jev selected it. Use the host's installed skill name for the handoff: the `grill-me` route uses the `grilling` skill when that is the installed name; `grill-with-docs` and `wayfinder` use their matching skills. At completion, identify the workflow steps that used Jev; say when routing was done by Codex because Jev was unavailable or the user chose the route directly.

## 2. Clarify decisions in Plannotator

Inspect the target project's `AGENTS.md`, current code, terminology, and documentation before asking for facts that can be found there. Invoke the chosen workflow by its installed skill name and use it to identify unresolved decisions.

For each decision round, show all independent questions on the current frontier together in Plannotator's scrollable interview form. Keep dependent questions for later rounds. Each question should be concise, include a recommended answer and useful options, and offer a custom text answer. Use single-select/custom or multi-select/custom modes as appropriate so the user can replace suggestions with their own answer. The user must be able to review earlier answers in the same round before submitting.

Use the `plannotator-setup-goal` skill to prepare the interview bundle and its `setup-goal interview` UI, but run only the interview phase. Put the temporary `goals/<slug>/` bundle and result in an isolated temporary workspace, not the project; do not create a project goal package or continue to facts/planning. Remove temporary files after resolving the round. Wait for the user to submit or dismiss the session. If Plannotator is unavailable, explain that and continue with a concise chat round.

Read every submitted answer and note. Address a blocking question or uncertainty before advancing to the next round. Skip the interview when the request and project context already settle the decisions.

## 3. Preserve useful project knowledge

Follow the target project's existing documentation conventions. Keep its glossary current with domain terms that will help future work, and record consequential design tradeoffs as ADRs. Prefer updating existing files over adding duplicates. If no convention exists, use the project's root `CONTEXT.md` for the glossary and `docs/adr/` for ADRs; create entries only when the work adds durable terminology or decisions.

When `grill-with-docs` is selected, inspect the project after the nested skill call and verify the expected glossary/ADR changes actually exist. If the nested skill did not write them, make the missing updates yourself. Carry accepted glossary terms and ADR decisions into any spec or tickets.

## 4. Plan and implement through existing skills

Choose follow-on skills according to the requested outcome and project setup. Use `to-spec` when a durable implementation spec is useful, `to-tickets` for multi-slice tracked work, and `implement` when the user wants the change built. Use `code-review` when the implementation workflow or user requests it. Avoid running the entire suite for a small change that does not need it.

`wayfinder` is a planning workflow. If the user asked only for a map or plan, stop at that boundary. If they asked to ship the work, continue from the resolved map into the appropriate spec, ticket, and implementation steps. Respect each selected skill's limits, the project's instructions, and any configured tracker; do not turn a plan-only request into code changes.

Invoke selected skills by their exact names when the host supports skill invocation. If it does not, follow the installed skill instructions directly and state that you used the instructions rather than invoking the skill. If a selected skill is missing, do not silently claim it ran.

Follow the target project's delegation rules before any selected skill spawns an agent or research worker. Keep complex design reasoning with Codex; reserve Jev for the bounded choices described above.

## 5. Teach back the implementation in Plannotator

After implementation, present a compact Plannotator walkthrough with these sections, in order:

1. **What started this work** — the request or problem that triggered it.
2. **Goal** — the outcome the user wanted.
3. **What we did** — the main behavioral changes and how the important pieces work together, with only the code touchpoints needed to make the explanation clear.
4. **Result** — what the user can now do or what changed in the system.

For a code change, use `plannotator-visual-explainer`'s PR/code-change walkthrough path and deliver the HTML through Plannotator's annotation UI. Keep the four sections above as the walkthrough's spine, adding only visual detail that improves understanding. Explain the main behavior/data flow and the reasons for important decisions. If there is no usable diff, show the same four-part walkthrough as a temporary Markdown document with `plannotator annotate`. If Plannotator or its walkthrough path is unavailable, present the same compact four-part walkthrough in chat. Do not let a UI failure skip the teach-back. Keep it compact; do not produce a line-by-line tour. Share or publish it only if the user asks.

After the walkthrough, let the user ask questions in chat and answer them directly. When they ask for a final recap, include the four sections plus the questions and answers from this work session. Save the teach-back as a project document only when they ask; include the recap and Q&A they requested and follow the project's documentation conventions.

## 6. Finish clearly

Keep status updates and handoffs short. After the Plannotator teach-back, invite questions without repeating the whole walkthrough in chat. On a requested final recap, repeat the four sections and include the questions and answers from this work session; mention verification or remaining limits only when they materially affect the explanation. Identify which steps used Jev. Do not claim that a skill, review, command, or test ran unless it did.
