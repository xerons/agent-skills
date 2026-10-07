---
name: dev-coach
description: Use when the user explicitly invokes `$dev-coach` in Codex or explicitly asks another host to use the dev-coach skill for end-to-end development help.
disable-model-invocation: true
---

# Dev Coach

Use this workflow only when the user explicitly invokes `$dev-coach` in Codex or explicitly asks another host to load/use the `dev-coach` skill. It is an end-to-end development guide: clarify the work, choose the right existing workflow, help implement it, and offer a permission-gated multi-format explanation when implementation is complete. The explanation is agent-led; do not quiz the user or require them to explain the code back.

## 1. Discover and clarify

Call `dev-discovery` with the user's request, settled preferences, relevant project facts, and requested outcome. It owns route selection, decision interviews, and glossary/ADR updates, then returns a pre-implementation handoff. If the user asked only for discovery or a map, stop at that boundary. If the selected route requires the explicit `/wayfinder` command, give the user that handoff and resume when they return with its result.

## 2. Plan and implement through existing skills

Choose follow-on skills according to the requested outcome and project setup. Use `to-spec` when a durable implementation spec is useful, `to-tickets` for multi-slice tracked work, and `implement` when the user wants the change built. Use `code-review` when the implementation workflow or user requests it. Avoid running the entire suite for a small change that does not need it.

`wayfinder` is a planning workflow. If the user asked only for a map or plan, stop at that boundary. If they asked to ship the work, continue from the resolved map into the appropriate spec, ticket, and implementation steps. Respect each selected skill's limits, the project's instructions, and any configured tracker; do not turn a plan-only request into code changes.

Invoke selected skills by their exact names when the host supports skill invocation. If it does not, follow the installed skill instructions directly and state that you used the instructions rather than invoking the skill. If a selected skill is missing, do not silently claim it ran.

Follow the target project's delegation rules before any selected skill spawns an agent or research worker. Keep complex design reasoning with the primary reasoning agent.

## 3. Offer a multi-format explanation

After implementation and any requested code-simplification pass, consider whether an explainer would improve the user's understanding. If the user explicitly asked for a teach-back for this work, invoke `multi-format-explainer` with the original request, goal, final code changes, important decisions, verification, and Jev-supported steps. Otherwise ask, “Would you like a multi-format explanation of the completed changes?” Wait for an explicit yes before invoking the skill. Do not treat invoking `dev-coach` as consent. If the user declines, finish with the normal implementation report. A nested `code-simplify` pass defers this offer to `dev-coach`.

## 4. Finish clearly

Keep status updates and handoffs short. After an approved explainer, invite questions without repeating the walkthrough in chat. On a requested final recap, include the four sections and the questions and answers from this work session; mention verification or remaining limits only when they materially affect the explanation. Identify which steps used Jev, including format selection when applicable. Do not claim that a skill, review, command, or test ran unless it did.
