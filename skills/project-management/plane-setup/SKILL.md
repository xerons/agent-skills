---
name: plane-setup
description: Use when explicitly creating a Plane project and configuring confirmed project capabilities for its workflow.
disable-model-invocation: true
---

# Plane Setup

Create a new Plane project and configure only the capabilities needed for the user's stated workflow or approved backlog. Setup creates the project shell; it does not publish epics or stories.

## Workflow

1. **Resolve the destination.** Confirm the Plane workspace, project name and identifier, and any requested lead, visibility, or process settings. Use context where clear; ask concise questions for missing details. Verify the authenticated principal, immutable workspace ID, and project-creation permission through the integration. If identity or destination cannot be verified, stop before writes.
2. **Inspect current configuration.** Read the workspace and relevant project defaults before proposing changes. If an approved backlog is supplied, use it to determine which capabilities are needed.
3. **Present the setup summary.** Show the acting account, immutable workspace ID/link, project details, each feature change, and its project/team/workspace scope. Bind any approval to these exact details. A clear request to create the named project authorizes that creation. Obtain explicit confirmation before changing shared team/workspace settings or any irreversible setting. Keep workspace hierarchy disabled unless specifically requested and confirmed with its workspace-level impact.
4. **Create and configure.** Before creation, search the exact workspace ID and project identifier; if the project already exists, report it instead of creating another. Revalidate the acting account and destination immediately before each write. If the account or destination differs from the approved summary, invalidate that approval, stop, present the new IDs and scope, and obtain confirmation again before any write. Use the configured official Plane MCP/API/CLI operations. When epics are needed, enable project Work Item Types and resolve the `Epic` type at project scope. Check cycle availability before using cycles. Create milestone records only when named in approved artifacts or requested. Configure modules only when requested or present in approved artifacts. Do not change workflow states, estimates, labels, priorities, or permissions based on guesses. If a create response is uncertain, read/search by exact workspace and project identifier before considering a retry.
5. **Read back and report.** Read the project and relevant feature state after the changes. Report the project identifier/link, confirmed settings applied, and anything unavailable or left unchanged. If a write partially succeeds, report exact results and stop before retrying a broad setup batch. After the completed report, offer `multi-format-explainer` when a teach-back would help. Wait for an explicit yes before invoking it; the project setup request does not authorize this handoff. If declined, finish with the normal report.

## Plane-specific rules

- Plane Epics are work items with type `Epic`; stories/tasks are work items linked through the parent relationship.
- Use the project Work Item Types capability for Epic support. Do not depend on a legacy separate Epics toggle unless current official Plane documentation confirms it is required.
- A milestone is a project checkpoint record, not a project feature toggle. A cycle represents sprint cadence; do not invent a schedule.
- Never enable workspace hierarchy as routine project setup.
- If the host exposes Plane MCP tools, use the corresponding project, work-item-type, work-item, milestone, and cycle operations. Tool availability does not authorize changes beyond the requested scope.

If the integration, permission, or required feature is unavailable, stop before the unsupported write and give the user the exact manual next step. After that report, offer `multi-format-explainer` if useful and wait for an explicit yes before invoking it; if declined, finish with the manual next step. Do not claim setup succeeded without a successful result and read-back. Setup uses explicit project/workspace facts and does not need Jev; report “Jev not used” for setup. If the user accepts the separate explainer handoff, that skill reports its own Jev use independently.
