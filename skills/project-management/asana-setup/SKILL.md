---
name: asana-setup
description: Use when explicitly creating an Asana project or configuring confirmed project-level workflow features in an existing project.
disable-model-invocation: true
---

# Asana Setup

Create a new Asana project or prepare an explicitly selected existing project, configuring only the project-local features needed for the user's stated workflow or approved backlog. Setup does not publish epics, stories, or milestones.

## Workflow

1. **Resolve the operation and destination.** Determine whether the user asked to create a new project or configure an existing one. Confirm the workspace or organization; in create mode, confirm the project name and (for an organization) the team that should have access; in configure-existing mode, resolve the exact project ID and read its current team membership. Resolve requested privacy, project view, and workflow details from the user's instructions; ask only for missing details that affect the destination or writes. Verify the authenticated principal, immutable workspace/project IDs, and required permission. Stop before writes if identity, destination, or permission cannot be verified.
2. **Inspect and propose.** Read current project defaults that affect the requested setup. In create mode, check exact workspace/project name matches; if the name already exists, show matching IDs and ask whether to choose another name or explicitly switch to configure-existing mode. Do not silently reuse an existing project. In configure-existing mode, operate only on the project the user selected by ID or an unambiguous exact name. Present a concise setup summary with acting account, workspace/team/project IDs, project visibility, each proposed setting, its scope, and any plan-gated feature. Project creation for the clearly named destination is authorized by the request. Obtain explicit approval before changes to an existing project's settings, team/workspace-wide settings, sharing beyond the specified team, or any other setting broader than the new project.
3. **Create when requested.** In create mode, revalidate the principal and workspace immediately before creation. Asana projects are bound to their workspace when created. For organization workspaces, use the current membership operation to share the project with the specified team; do not rely on deprecated project-create team/privacy parameters. In configure-existing mode, do not create a project. If the destination or principal changed since the summary, stop and present the new scope for approval.
4. **Configure approved project-local features.** Create only requested or backlog-supported sections and local custom fields in the selected project. For the selected Scrum profile, represent named cycle values in a project-local `Sprint` single-select field; create options only from explicitly supplied cycle names. Map supplied estimates to a local number or single-select field only when the values and units fit exactly. Map supplied release names to a local `Release` field, not to a made-up native release object. Do not add local fields to the workspace field library. Epics need no special Asana type: publishing represents an epic as a parent task. Milestone records are created by `asana-publish`, not setup. Never create task records during setup.
5. **Read back and report.** Re-read the project, membership, sections, and custom-field settings that were written. Report the project ID/link, effective team/visibility, confirmed local features, and anything unavailable. If a write partially succeeds or its result is uncertain, report exact results and stop before retrying the setup batch. After the completed report, offer `multi-format-explainer` when a teach-back would help. Wait for an explicit yes before invoking it; the project setup request does not authorize this handoff. If declined, finish with the normal report.

## Asana-specific rules

- Keep the workflow in one project. Do not create a portfolio, feature projects, backlog project, or sprint projects as part of this profile.
- Sections represent workflow stages only when those stages were requested or approved. The project-local `Sprint` field carries sprint assignment so sections remain available for workflow.
- A project-local custom field must be attached to this project only. Asana also supports workspace-wide fields; do not create or modify those for routine setup.
- Creating an organization project requires a selected team membership. Confirm the team and use the current membership API/tool after project creation; project workspace cannot be changed later.
- A milestone is a task type representing one point in time and cannot have a start date. Setup does not create milestones.
- Do not change default assignees, dates, privacy, workflow stages, or permissions based on guesses.
- If the host has no authenticated Asana MCP/API/CLI integration, make no writes and provide a concise manual setup checklist. Do not claim creation or configuration without successful results and read-back. After the checklist, offer `multi-format-explainer` if useful and wait for an explicit yes before invoking it; if declined, finish with the checklist.
- Setup uses explicit project/workspace facts and does not need Jev; report “Jev not used” for setup. If the user accepts the separate explainer handoff, that skill reports its own Jev use independently.

## Official references

- [Asana for Agile and Scrum](https://help.asana.com/s/article/asana-for-agile-and-scrum)
- [Create a project](https://developers.asana.com/reference/createproject)
- [Create a membership](https://developers.asana.com/reference/createmembership)
- [Custom fields guide](https://developers.asana.com/docs/custom-fields-guide)
- [Add a custom field to a project](https://developers.asana.com/reference/addcustomfieldsettingforproject)
- [Create a section in a project](https://developers.asana.com/reference/createsectionforproject)
