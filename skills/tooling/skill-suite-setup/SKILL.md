---
name: skill-suite-setup
description: Use when the user explicitly asks to install or prepare selected skills from the xerons/agent-skills collection, including their external skill, CLI, MCP, or account prerequisites.
---

# Skill Suite Setup

Set up only the skills and prerequisites the user asks for. This skill is the collection's bootstrap helper: it has no dependency on Jev, Plannotator, or any other collection skill.

## Workflow

1. **Resolve the request.** Read `references/setup-matrix.md`. Default to the current agent host and global installation; support Codex and OpenCode. Honor an explicitly named agent or scope. If the user names skills, use those exact names. If they describe an outcome, match it to the collection skills; use Jev to rank plausible skill matches when available, then ask one short question if the choices remain unclear. Exact command names and environment checks do not need Jev.
2. **Inspect current setup.** Check installed skills with `npx skills list --global --agent <agent>` (use the requested agent and scope). Check selected local CLIs with `command -v`. Use the current session's available tool inventory to check for MCP tools. Session visibility only proves availability in this session; do not claim a service is unconfigured globally based on missing tools here. Do not read raw credential files.
3. **Show a concise setup plan.** Separate collection skills, external skills, local CLIs, and MCP/account connections. Mark each as installed, missing, optional, or not verifiable. Include the exact install command and explain host-level changes before making them. Skip prerequisites that are already satisfied.
4. **Install selected skills.** Once the user has named the selection or accepted the plan, install only those collection skills with `npx skills add xerons/agent-skills --skill <name> --agent <agent> --global`, repeating `--skill <name>` for each. Use `codex` or `opencode` as the agent value. Install only the external skills needed for the selected workflow, using the verified source and command in the setup matrix. Never use `--skill '*'` unless the user asked for the full collection. Do not install system tools or run a remote shell installer without first showing its official command and getting the user's confirmation.
5. **Guide connections.** Direct MCP and OAuth setup through the agent host's connection flow. In OpenCode, use its current `opencode mcp` command or version-matched configuration instructions; summarize host-level changes before making them. Never ask the user to paste a key or token, write credentials to project files, or modify MCP configuration silently. Wait for the user to finish an interactive sign-in when needed.
6. **Verify and report.** Re-list installed skills and re-check available local CLIs and current-session MCP tools where possible. Report what is ready, what still needs user sign-in or manual setup, what could not be verified, and any unavailable optional fallback. Recommend a fresh Codex session or restart OpenCode if newly installed skills are not yet visible.

## Guardrails

- Running this skill requires an explicit setup request. Discussing a skill or reading this guide alone does not authorize installation.
- Keep the setup matrix as the source for dependency names and official setup links; do not guess package names, MCP identifiers, or install commands.
- Jev may help select skills from a natural-language goal. It does not verify that a CLI, skill, account, or MCP connection exists.
- If an MCP connection is missing and the matrix has no provider-specific instructions, report the gap and direct the user to the host's MCP settings; do not invent a server configuration.
- Installing a skill does not install its CLI or authenticate its services. Report those as separate prerequisites.
- Leave credentials in the user's host-managed credential store. Do not print, copy, or commit them.
