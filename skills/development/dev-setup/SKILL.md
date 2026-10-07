---
name: dev-setup
description: Use when the user asks to prepare a repository for AI-assisted development by creating or updating project-local agent instructions and context.
---

# Dev Setup

Prepare the current repository for the user's AI-assisted development workflow with minimal, reusable, repo-local guidance. Treat the user's request to set up the repo as authorization for the necessary local instruction-file edits described here. Keep tool installation and external account or service setup outside that scope.

## Workflow

1. **Choose the target.** Use the current repository and active agent host by default. Configure additional hosts only when the user names them. If the target repository or host cannot be inferred and changes would differ, ask one short question.
2. **Inspect before editing.** Read the root and relevant nested instructions, project overview, existing agent configuration, and documentation conventions. Use `dev-doctor` when available to reuse its evidence-backed audit; otherwise inspect the same areas directly. Follow higher-level and nested instructions that apply to each file.
3. **Find the actual gaps.** Derive project purpose and stack from repository evidence. Include only useful local context such as entry points, module ownership, established build or validation commands, conventions, and links to maintained docs. Treat missing files as a gap only when the requested workflow needs them. If setup is already adequate, leave it unchanged.
4. **Make the smallest useful update.** Prefer updating the appropriate existing instruction file. Add a file only when the active host has no suitable project-local entry point. Preserve unrelated content, respect nested instruction scope, avoid duplicate docs, and make rerunning setup safe. Use Jev for simple classification or ranking of evidence-backed gaps when available; the primary reasoning agent decides project-specific policy and verifies the source evidence.
5. **Keep setup local.** Do not copy global skills into the repo, install tools or skills, configure credentials, connect external services, add packages, or change CI/hooks as part of ordinary setup. If the user asks for one of these separately, handle only that explicit request through the appropriate workflow.
6. **Check and report.** Read back every changed file and confirm each referenced path or command exists in the repo. Do not run project builds or tests unless the user asks. Report the active host, files created or changed, why each was needed, checks actually performed, and any setup work left outside scope. If a visual or interactive explanation would materially improve understanding, ask permission before invoking `multi-format-explainer` and wait for an explicit yes. If the user declines, end with the normal setup report.

Ask about a genuine project choice when repository evidence cannot settle it. Do not make broad policy decisions, replace existing instructions, or add boilerplate to make the setup look complete.
