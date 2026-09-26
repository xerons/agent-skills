# Agent Skills

Personal agent skills organized by group. Each skill lives in its own folder and contains a `SKILL.md` entry point.

## Install

Use the [`skills` CLI](https://github.com/vercel-labs/skills) to install skills from this repository into Codex. List available skills, then install one or more globally:

```sh
npx skills add xerons/agent-skills --list
npx skills add xerons/agent-skills --skill dev-coach --agent codex --global
```

Repeat `--skill` to select multiple skills. To install the full collection or update existing global installs:

```sh
npx skills add xerons/agent-skills --skill '*' --agent codex --global
npx skills update -g
```

These commands install skill files only. Required tools, MCP connections, and authentication are listed below. Install from GitHub after pushing the changes you want to use.

## Development

- **dev-coach** — guides development work from clarification through implementation and teach-back.
- **code-simplify** — simplifies recently changed code while preserving behavior.
- **dev-doctor** — audits a repository's AI-assisted development setup.
- **dev-setup** — prepares a repository with minimal, project-local agent guidance.
- **repo-map** — explains repository structure and important code paths.

## Project Management

- **tpm-spec** — shapes an initiative into an approved, tracker-neutral spec and epic/story backlog.
- **plane-setup** — creates a Plane project and configures confirmed process features.
- **plane-publish** — previews and publishes approved backlog items to an existing Plane project.
- **linear-setup** — creates a Linear project and configures confirmed process features.
- **linear-publish** — previews and publishes approved backlog items to an existing Linear project.
- **asana-setup** — creates an Asana project or configures confirmed project-local workflow features.
- **asana-publish** — previews and publishes approved backlog items to one existing Asana project.

## Tool and connection setup

The `*-setup` tracker skills configure tracker projects; they do not install or authenticate an MCP server. Connect the relevant integration in the agent host you use. Keep API keys, personal access tokens, OAuth client secrets, and access tokens in the host's credential store or another private location, never in this repository.

| Skill | Required tools and access |
| --- | --- |
| `dev-coach` | Local repository access; TypeSafe Jev for preferred route selection; Plannotator CLI plus `plannotator-setup-goal`, `plannotator-visual-explainer`, and `plannotator-annotate` for the guided interview and teach-back UI; and the selected route skill (`grilling` for grill-me, `grill-with-docs`, or `wayfinder`). It falls back to chat when Plannotator is missing. External skills are not bundled here. |
| `code-simplify` | Read/write access to the target repository and its normal editing tools. No tracker connection or API credential. |
| `dev-doctor` | Read access to repository instructions and agent/tool inventory. TypeSafe Jev is used for evidence-backed finding priority when available; Codex can classify if it is unavailable. |
| `dev-setup` | Read/write access to the target repository. `dev-doctor` and TypeSafe Jev improve the workflow but are not required to make local instruction updates. It does not install tools or configure credentials. |
| `repo-map` | Read-only repository search and file access. TypeSafe Jev helps rank candidate files when useful; local search is the fallback. |
| `tpm-spec` | Read/write access to the selected project documentation directory. No tracker connection. TypeSafe Jev may assist with bounded judgments under the recorded preference. |
| `plane-setup` | Authenticated Plane MCP, API, or CLI access that can inspect the workspace and create/configure the requested project. Plane's remote MCP supports OAuth; its PAT route requires a token and workspace slug. |
| `plane-publish` | Authenticated Plane MCP, API, or CLI access that can read the target project and create approved work items. Use existing project features for cycles and milestones; publishing does not enable workspace/team settings. |
| `linear-setup` | Authenticated Linear MCP or API access that can create a project. Team-level changes such as enabling Cycles require the appropriate team permission and separate approval. |
| `linear-publish` | Authenticated Linear MCP or API access that can read the target project and create approved issues. Use an existing cycle; publishing does not enable team-level features. |
| `asana-setup` | Authenticated Asana MCP or API access that can create a project or configure project-local features. Asana's V2 MCP uses an OAuth app; standard API access uses a separate API app or PAT. |
| `asana-publish` | Authenticated Asana MCP or API access that can read the target project and create approved tasks, subtasks, milestones, and dependencies. |

### Official tracker connection guides

- [Plane MCP server](https://developers.plane.so/dev-tools/mcp-server) — OAuth for interactive clients; PAT authentication is an alternative.
- [Linear MCP server](https://linear.app/docs/mcp) — interactive OAuth is supported; API keys are an alternative. These publishing workflows need write access.
- [Asana MCP integration](https://developers.asana.com/docs/integrating-with-asanas-mcp-server) — V2 uses a pre-registered OAuth app and tokens for the MCP server. For Codex-specific configuration, see [Connecting coding clients to Asana's V2 server](https://developers.asana.com/docs/connecting-mcp-clients-to-asanas-v2-server).

`dev-setup` is for repository-local agent guidance, not MCP installation or account connection. A separate interactive connection skill may be useful if you repeatedly set up the same tracker integrations across different agent hosts; for now, the README points to each vendor's current, host-specific instructions without handling secrets.

## Local dependencies

`skills-lock.json` records external skills used while developing this collection, including `typesafe-ai`. `.agents/skills/` contains local installed copies and is not tracked.
