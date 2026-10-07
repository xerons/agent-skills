# Skill Suite Setup Matrix

This is the dependency reference for `skill-suite-setup` and the repository README. Set up only prerequisites needed for the skills selected by the user.

## Collection skill installation

Install selected skills globally for the active supported host. The `skills` CLI accepts `codex` and `opencode` as the `--agent` value:

```sh
npx skills add xerons/agent-skills --skill <skill-name> --agent opencode --global
```

Repeat `--skill <skill-name>` for each selected skill. Replace `opencode` with `codex` to target Codex. OpenCode loads standard `SKILL.md` files through its [native skill tool](https://opencode.ai/docs/skills); its global skill directory is `~/.config/opencode/skills/`. The `skill-suite-setup` skill itself requires Node.js/npm's `npx` and access to the public GitHub repository; it has no MCP, external-skill, or Plannotator dependency.

## Per-skill prerequisites

| Skill | Prerequisites |
| --- | --- |
| `skill-suite-setup` | `npx` and access to the collection repository. No external skill, CLI, MCP, or credential is required to bootstrap. |
| `multi-format-explainer` | No mandatory external skill, Jev connection, or media-generation tool. It adapts to available tools; Jev can choose among feasible formats, while diagrams, interactive HTML, and video depend on host capabilities. |
| `dev-discovery` | Local project access; Matt's `grilling` skill for interview routes and `domain-modeling` for glossary/ADR work. Plannotator plus `plannotator-setup-goal` provides the preferred browser interview; HTML is a fallback when the host can return form answers, with chat as the final fallback. `ask-matt` is user-invoked and recommends a route without running it, so `dev-discovery` applies its route distinctions directly; users can install `ask-matt` for direct access. The Wayfinder route requires installing and explicitly invoking `wayfinder`; it owns its multi-session map and ticket process. |
| `dev-coach` | Local project access; `dev-discovery` for clarification; optional follow-on skills are `to-spec`, `to-tickets`, `implement`, and `code-review`. Install `multi-format-explainer` too if you want its optional teach-back; it has no mandatory external dependencies. |
| `code-simplify` | Read/write access to the target repository and its normal editing tools. No tracker connection or API credential. |
| `dev-doctor` | Read access to repository instructions and the agent/tool inventory. Jev is optional for evidence-backed finding priority; the primary reasoning agent can classify when Jev is unavailable. |
| `dev-setup` | Read/write access to the target repository. `dev-doctor` and Jev can improve the workflow but are not required to edit local instructions. It does not install tools or configure credentials. |
| `repo-map` | Read-only repository search and file access. Jev can rank candidate files when useful; local search is the fallback. |
| `tpm-spec` | Read/write access to the selected project documentation directory. No tracker connection is required. Jev may assist with bounded judgments under the recorded preference. |
| `plane-setup` | Authenticated Plane MCP, API, or CLI access that can inspect the workspace and create/configure the requested project. Plane's remote MCP supports OAuth; its PAT route requires a token and workspace slug. |
| `plane-publish` | The `tpm-spec` skill plus authenticated Plane MCP, API, or CLI access that can read the target project and create approved work items. Use existing project features for cycles and milestones; publishing does not enable workspace/team settings. |
| `linear-setup` | Authenticated Linear MCP or API access that can create a project. Team-level changes such as enabling Cycles require the appropriate team permission and separate approval. |
| `linear-publish` | The `tpm-spec` skill plus authenticated Linear MCP or API access that can read the target project and create approved issues. Use an existing cycle; publishing does not enable team-level features. |
| `asana-setup` | Authenticated Asana MCP or API access that can create a project or configure project-local features. Asana's V2 MCP uses an OAuth app; standard API access uses a separate API app or PAT. |
| `asana-publish` | The `tpm-spec` skill plus authenticated Asana MCP or API access that can read the target project and create approved tasks, subtasks, milestones, and dependencies. |

## External skill and CLI setup

### TypeSafe and Jev

Install the TypeSafe skill from the [official TypeSafe skills repository](https://github.com/typesafe-ai/skills), targeting the active host:

```sh
npx skills add typesafe-ai/skills --skill typesafe-ai --agent opencode --global
```

Replace `opencode` with `codex` to target Codex.

The skill provides TypeSafe guidance; it does not itself make Jev tools available. Connect a Jev MCP server in the host and check that the selected workflows' expected Jev tools appear in the current session (for example, a format-selection tool for `multi-format-explainer`, a semantic-search tool for `repo-map`, or a classification tool for `dev-doctor`). OpenCode may namespace MCP tool names differently from Codex, so check the current tool inventory instead of requiring a specific identifier. See the [OpenCode MCP documentation](https://opencode.ai/docs/mcp-servers) for its connection flow. Jev is an optional fallback for skills that explicitly permit the active agent to classify when unavailable. Do not infer global MCP configuration from current-session tool visibility.

### Matt Pocock workflow skills

Install only the selected route and its supporting skills from [`mattpocock/skills`](https://github.com/mattpocock/skills), targeting the active host:

```sh
npx skills add mattpocock/skills --skill grilling --skill domain-modeling --agent opencode --global
npx skills add mattpocock/skills --skill grill-me --skill grilling --agent opencode --global
npx skills add mattpocock/skills --skill grill-with-docs --skill grilling --skill domain-modeling --agent opencode --global
npx skills add mattpocock/skills --skill wayfinder --skill grilling --skill domain-modeling --agent opencode --global
npx skills add mattpocock/skills --skill ask-matt --agent opencode --global
```

Replace `opencode` with `codex` to target Codex.

Run one command for the route the user selected. `wayfinder` can use a tracker or local Markdown; configure tracker access only when the user wants tracker-backed work.

The `dev-coach` handoffs can also use `to-spec`, `to-tickets`, `implement`, and `code-review`. Install only the follow-on skills the user wants:

```sh
npx skills add mattpocock/skills --skill to-spec --skill to-tickets --skill implement --skill code-review --agent opencode --global
```

Replace `opencode` with `codex` to target Codex.

### Plannotator

For macOS, Linux, or WSL, the official full installer is:

```sh
curl -fsSL https://plannotator.ai/install.sh | bash
```

See [Plannotator installation instructions](https://github.com/backnotprop/plannotator#install) for current platform-specific steps. The full installer supports multiple agents and provides the Plannotator CLI and core skills. For OpenCode, also add the Plannotator plugin using the configuration format for the installed OpenCode version, then restart OpenCode. The plugin is required for the OpenCode plan-review integration; installing the CLI alone does not configure it. The optional setup-goal and visual-explainer skills are distributed separately; install only the selected ones for the active host:

```sh
npx skills add https://github.com/backnotprop/plannotator/tree/main/apps/skills/extra/plannotator-setup-goal --agent opencode --global
npx skills add https://github.com/backnotprop/plannotator/tree/main/apps/skills/extra/plannotator-visual-explainer --agent opencode --global
```

Replace `opencode` with `codex` to target Codex.

For OpenCode plugin setup and version-specific configuration, follow [Plannotator's OpenCode instructions](https://github.com/backnotprop/plannotator/tree/main/apps/opencode-plugin). Its installer also provides OpenCode command stubs for `/plannotator-review`, `/plannotator-annotate`, and `/plannotator-last`.

The installer and extra-skill source can update home-level files. Show the commands and their effects before running them; execute only after the user confirms.

## Tracker connection guides

- [Plane MCP server](https://developers.plane.so/dev-tools/mcp-server) — OAuth for interactive clients; PAT authentication is an alternative.
- [Linear MCP server](https://linear.app/docs/mcp) — interactive OAuth is supported; API keys are an alternative. Publishing needs write access.
- [Asana MCP integration](https://developers.asana.com/docs/integrating-with-asanas-mcp-server) — V2 uses a pre-registered OAuth app and tokens for the MCP server. For Codex-specific configuration, see [Connecting coding clients to Asana's V2 server](https://developers.asana.com/docs/connecting-mcp-clients-to-asanas-v2-server).
- [OpenCode MCP servers](https://opencode.ai/docs/mcp-servers) — configure project or global MCP connections and authenticate from OpenCode.

The tracker `*-setup` skills configure tracker projects; they do not install or authenticate an MCP server. Keep API keys, personal access tokens, OAuth client secrets, and access tokens in the host's credential store or another private location, never in this repository.
