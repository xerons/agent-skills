# Agent Skills

Personal agent skills organized by group. Each skill lives in its own folder and contains a `SKILL.md` entry point.

## Install

The skills use the standard `SKILL.md` format and work in Codex and OpenCode. Use the [`skills` CLI](https://github.com/vercel-labs/skills) to install the setup helper for the agent you use:

```sh
npx skills add xerons/agent-skills --skill skill-suite-setup --agent opencode --global
```

For Codex, replace `opencode` with `codex`. In Codex, invoke the helper with `$skill-suite-setup`. In OpenCode, ask the agent to use the `skill-suite-setup` skill. It can install the selected collection skills and guide their external tools and connections. The helper itself does not depend on Jev, Plannotator, or any other skill in this collection.

You can also list skills and install them directly. Repeat `--skill` to select multiple skills; use `'*'` for the full collection:

```sh
npx skills add xerons/agent-skills --list
npx skills add xerons/agent-skills --skill dev-coach --agent opencode --global
npx skills add xerons/agent-skills --skill '*' --agent opencode --global
npx skills update -g
```

Replace `opencode` with `codex` to target Codex.

These commands install skill files only. Install from GitHub after pushing the changes you want to use.

## Development

- **dev-coach** — guides development work through discovery and implementation, with an optional teach-back.
- **dev-discovery** — independently clarifies a software idea and returns a pre-implementation handoff.
- **multi-format-explainer** — explains a topic or completed result in prose, diagrams, interactive HTML, or video when suitable tools are available.
- **code-simplify** — simplifies recently changed code while preserving behavior.
- **dev-doctor** — audits a repository's AI-assisted development setup.
- **dev-setup** — prepares a repository with minimal, project-local agent guidance.
- **repo-map** — explains repository structure and important code paths.

## Tooling

- **skill-suite-setup** — installs selected collection skills and guides setup of their required tools and connections in Codex or OpenCode.

## Project Management

- **tpm-spec** — shapes an initiative into an approved, tracker-neutral spec and epic/story backlog.
- **plane-setup** — creates a Plane project and configures confirmed process features.
- **plane-publish** — previews and publishes approved backlog items to an existing Plane project.
- **linear-setup** — creates a Linear project and configures confirmed process features.
- **linear-publish** — previews and publishes approved backlog items to an existing Linear project.
- **asana-setup** — creates an Asana project or configures confirmed project-local workflow features.
- **asana-publish** — previews and publishes approved backlog items to one existing Asana project.

## Tool and connection setup

The [skill setup matrix](skills/tooling/skill-suite-setup/references/setup-matrix.md) lists each skill's required tools, external skills, MCP access, and official tracker connection guides. [OpenCode discovers skills](https://opencode.ai/docs/skills) in its global or project skill directories and loads them through its skill tool; Codex uses its own skill discovery and `$skill-name` invocation. The `*-setup` tracker skills configure tracker projects; they do not install or authenticate an MCP server. Keep API keys, personal access tokens, OAuth client secrets, and access tokens in the host's credential store or another private location, never in this repository.

`dev-setup` prepares repository-local agent guidance. `skill-suite-setup` prepares the personal skill collection and its prerequisites.

## Local dependencies

`skills-lock.json` records external skills used while developing this collection, including `typesafe-ai`. `.agents/skills/` contains local installed copies and is not tracked.
