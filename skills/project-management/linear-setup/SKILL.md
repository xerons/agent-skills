---
name: linear-setup
description: Use when explicitly creating a Linear project and configuring confirmed project or team capabilities for its workflow.
disable-model-invocation: true
---

# Linear Setup

Create a new Linear project and configure only capabilities needed for the user's stated workflow or approved backlog. Setup creates the project shell; it does not publish backlog issues.

## Workflow

1. **Resolve the destination.** Confirm the Linear workspace, team, project name, and any requested lead, visibility, or process settings. Use context where clear and ask concise questions for missing details. Verify the authenticated principal, immutable workspace/team IDs, and project-creation permission through the integration. Generate a local setup operation key before creation and use it as a request idempotency key if the integration supports one. If identity or destination cannot be verified, stop before writes.
2. **Inspect current configuration.** Read team and project settings before proposing changes. Use an approved backlog, if supplied, to identify required capabilities.
3. **Present the setup summary.** Show the acting account, immutable workspace/team IDs and links, project details, and each proposed feature change with its scope. Bind approval to these exact details. A clear request to create the named project authorizes that creation. Obtain explicit confirmation before changing shared team/workspace settings or any irreversible setting.
4. **Create and configure.** Before creation, search the exact workspace/team IDs and project name. If one or more same-name projects exist, stop and ask the user to select the intended project or choose a distinct name. Revalidate the acting account and destination immediately before each write. If the account or destination differs from the approved summary, invalidate that approval, stop, present the new IDs and scope, and obtain confirmation again before any write. Create the project in the named team with the operation idempotency key when supported, then apply only confirmed settings. If the user wants Scrum cycles and Cycles are disabled, explain that enabling them changes team settings and get explicit confirmation first. Ask for cycle duration and start day if not already configured. Create project milestones only when named in approved artifacts or requested. Do not enable Initiatives or configure Releases by default. If a create response is uncertain, search by the operation key; if unsupported, use exact workspace/team/name and creator/time metadata. Recover only one unambiguous project created by the current operation. If the result cannot be uniquely established, stop and ask the user instead of retrying.
5. **Read back and report.** Read the project and relevant team/project feature state. Report the project identifier/link, settings applied, and anything unavailable or left unchanged. If a write partially succeeds, state exact results and stop before retrying a broad setup batch.

If no authenticated Linear integration is available, stop before any write and provide a concise setup checklist. Never claim the project exists without a successful result and read-back. Setup uses explicit project/team facts and does not need Jev; report “Jev not used.”
