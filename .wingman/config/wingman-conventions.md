# Wingman Workspace Conventions

This is Wingman-managed operating guidance. Project initialization refreshes this file from the installed Wingman builtin. Inspect it here, but put project-specific policies in registered `.wingman/rules/` entries rather than editing this file.

## Custom Project Rules

Use `rules_list` and `rules_get` to discover project standards. Register custom rule files in `.wingman/config/wingman.json` using `rules.active` and a named `rules.profiles` entry. Profiles with `at_session_start: true` are included at session start; rule frontmatter names are the profile references. Keep custom coding standards, design policy, privacy boundaries, and project decisions in these user-owned rules.

## Directory Schema

| Location | Purpose | Managed By |
| -------- | ------- | ---------- |
| .wingman/issues/ | Issue tracking files (markdown provider only) | Wingman MCP endpoints (markdown provider only) |
| .wingman/specifications/ | Feature specifications (markdown provider only) | Wingman MCP endpoints (markdown provider only) |
| .wingman/notes/ | Legacy/local note location; endpoint receipt defines actual storage | writing-notes / notes_create (receipt defines storage) |
| .wingman/memory/ | Agent-managed compacted knowledge base | Manual / future automation |
| .wingman/rules/ | Project rules and standards (coding, testing, security). Delivered to agent context via .claude/rules/ symlinks. | wingman:init-workspace |
| .wingman/plans/ | Implementation plans | wingman:writing-plans skill |
| .wingman/cache/ | Runtime cache | System |
| .wingman/workflow-state/ | Durable workflow-owned project state that must survive cache cleanup and disposable run worktrees | Manual |
| .wingman/config/ | Configuration files | wingman:init-workspace |
| .wingman/playbooks/ | Playbook assets for prompts, workflows, and templates | wingman:init-workspace |
| .wingman/sessions/ | Session state and history | MCP session tools |
| .wingman/rules/DESIGN.md | Detailed design philosophy and architectural guidelines | Manual |
| .wingman/rules/CODING.md | Language-specific coding conventions and patterns | Manual |
| .wingman/rules/TESTING.md | Test strategy, coverage goals, and testing patterns | Manual |
| .wingman/rules/SECURITY.md | Security policies, data handling, and threat model | Manual |
| .wingman/memory/decisions/ | Architecture Decision Records (ADRs) | adr-skill |

## Intent Routing

| When you need to... | Use this skill/tool |
| ------------------- | ------------------- |
| Write a note, memo, or research | wingman:writing-notes |
| Create or track a task/issue | wingman:creating-issues |
| Write a feature specification | wingman:writing-specifications |
| Create an implementation plan | wingman:writing-plans |
| Run tests | wingman:running-tests |
| Review code | wingman:reviewing-code |
| Commit, push, create PR | wingman:commit-push-pr |
| Run a workflow | wingman:running-workflows |

## Rules & Project Standards

Claude Code receives registered rules through `.claude/rules/` symlinks; other plugins resolve registered profiles. Use the relevant skills and rules through progressive disclosure.

- Always check for and use the relevant skill before creating files in .wingman/
- Ordinary requests such as "save a note" or "track this issue" select Wingman automatically; users need not name Wingman. Notes, memos, research, and idea notes go through the writing-notes skill and `notes_create`. Idea issues and tasks go through creating-issues and `issues_create`; updates use `issues_update`.
- Issues and specifications MUST be created and edited via MCP tools (issues_create, issues_update, etc.) -- never via `gh issue create` or hand-editing files, as the MCP tools handle project board linking and field metadata that the CLI does not. When the provider is `github` (check `.wingman/config/wingman.json`), MCP tools create GitHub issues. Use `type: specification` for specs and `type: issue` for tasks.
- The `.wingman/specifications/` and `.wingman/issues/` directories are only used by the markdown provider. When the GitHub provider is active, these directories are not the source of truth -- GitHub is.
- Confirm the intended project before writing. Respect the configured provider, including a markdown provider behind Wingman endpoints; metadata fields do not select storage.
- If the required tool is unavailable or fails, report that saving is not confirmed. Do not silently fall back to hand-written Markdown or direct GitHub creation, even if a bundled skill suggests that fallback. Explicit user requests for file exports remain valid. Inspect ambiguous results before retrying to avoid duplicates.
- Report the returned identifier/link and actual persistence receipt. A local receipt is not proof of gateway upload or replication. Never claim success merely because a request was attempted.
- The .wingman/memory/ directory is for reference material and knowledge base content, not for notes

## Source of Truth
- **Wingman Issues are source of truth** for what should be built. PRs reference specs/issues/epics, not the other way around.

## Workflow Observability

For details on running workflows, use Wingman MCP tool `skills_use({name:"running-workflows"})`. Workflow run history, status, transcripts, logs, metrics, child sessions, and status transitions are accessed through the gateway-backed MCP tools below.

- Use the workflow run ID as the primary handle for gateway-hosted work.
- Use `workflow_runs` to find runs, `workflow_detail` with `include: ["steps"]` for the canonical spine run record and step progress, `workflow_logs` for bounded step logs, and `workflow_transcript` for transcript tails. Use the dedicated cost endpoint/tool for cost; spine transcript, logs, and cost intentionally return typed unavailable/empty projections until those facts are persisted.
- Use `session_status({ sessionId: "<run-id>" })` only for a compact workflow/session summary. Do not treat it as a replacement for `workflow_detail` when diagnosing run state.
- If `workflow_detail` reports transcript paths with `pathLocality: "gateway-host"`, treat those paths as gateway-host-local paths. Read transcript content through `workflow_transcript` or `workflow_logs` when `readableViaApi` is true.

Use the running-workflows skill before launching workflows. A launch is not completion: retain the run ID and check the final status before claiming success.
