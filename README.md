# Agent Skills

Personal agent skills organized by group. Each skill lives in its own folder and contains a `SKILL.md` entry point.

## Install

Use the [`skills` CLI](https://github.com/vercel-labs/skills) to install the setup helper globally in Codex:

```sh
npx skills add xerons/agent-skills --skill skill-suite-setup --agent codex --global
```

Then invoke it in Codex, for example: `$skill-suite-setup Set up dev-coach and asana-publish.` It can install the selected collection skills and guide their external tools and connections. The helper itself does not depend on Jev, Plannotator, or any other skill in this collection.

You can also list skills and install them directly. Repeat `--skill` to select multiple skills; use `'*'` for the full collection:

```sh
npx skills add xerons/agent-skills --list
npx skills add xerons/agent-skills --skill dev-coach --agent codex --global
npx skills add xerons/agent-skills --skill '*' --agent codex --global
npx skills update -g
```

These commands install skill files only. Install from GitHub after pushing the changes you want to use.

## Development

- **dev-coach** — guides development work from clarification through implementation and teach-back.
- **code-simplify** — simplifies recently changed code while preserving behavior.
- **dev-doctor** — audits a repository's AI-assisted development setup.
- **dev-setup** — prepares a repository with minimal, project-local agent guidance.
- **repo-map** — explains repository structure and important code paths.

## Tooling

- **skill-suite-setup** — installs selected collection skills and guides setup of their required tools and connections in Codex.

## Project Management

- **tpm-spec** — shapes an initiative into an approved, tracker-neutral spec and epic/story backlog.
- **plane-setup** — creates a Plane project and configures confirmed process features.
- **plane-publish** — previews and publishes approved backlog items to an existing Plane project.
- **linear-setup** — creates a Linear project and configures confirmed process features.
- **linear-publish** — previews and publishes approved backlog items to an existing Linear project.
- **asana-setup** — creates an Asana project or configures confirmed project-local workflow features.
- **asana-publish** — previews and publishes approved backlog items to one existing Asana project.

## Tool and connection setup

The [skill setup matrix](skills/tooling/skill-suite-setup/references/setup-matrix.md) lists each skill's required tools, external skills, MCP access, and official tracker connection guides. The `*-setup` tracker skills configure tracker projects; they do not install or authenticate an MCP server. Keep API keys, personal access tokens, OAuth client secrets, and access tokens in the host's credential store or another private location, never in this repository.

`dev-setup` prepares repository-local agent guidance. `skill-suite-setup` prepares the personal skill collection and its prerequisites.

## Local dependencies

`skills-lock.json` records external skills used while developing this collection, including `typesafe-ai`. `.agents/skills/` contains local installed copies and is not tracked.
