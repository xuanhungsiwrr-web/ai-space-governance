---
name: ai-space-governance
description: Govern durable artifact placement, naming, source-of-truth, versioning, and handoff across anh Hưng's AI_Space. Use whenever ChatGPT or Codex plans, creates, edits, installs, packages, saves, moves, migrates, publishes, or decides the storage location for a persistent skill, plugin, MCP server, reusable tool, source repository, release, template, reference, document, report output/feedback pair, project workspace, guide, prompt, architecture decision, learning artifact, or platform configuration. Also use whenever work mentions AI_Space, xh-tuvan, xh-global-control, shared Claude/ChatGPT files, Google Drive canonical storage, GitHub source, or an artifact that must remain available after the current session. Do not use for a transient chat-only answer that creates no durable artifact.
---

# AI Space Governance

Apply anh Hưng's approved AI_Space storage policy without redesigning it.

## Required workflow

1. Before choosing a destination or writing any durable artifact, read [references/ai-space-policy.md](references/ai-space-policy.md) in full.
2. Classify the artifact by purpose, ownership, lifecycle, and canonical source.
3. Select one canonical destination from the policy. Do not create parallel editable copies.
4. For Google Drive writes, use the connected account's **My Drive** as the default scope. The canonical AI_Space root is folder ID `1WmAJH_H-VEXWrcuS-VJf2Xmr7Ov0TVQ_`. Never use folder ID `1rZQvJNOKSN9Ym7A8NwqMhw-gaP9ftVJB` as a default or fallback destination. Route AI_Space artifacts into the approved AI_Space tree rather than leaving them loose in the My Drive root. Treat the Drive folder ID as the canonical identity: a synced path such as `G:\My Drive\AI_Space` is only a local materialization after its mapping to that ID is verified, not proof of the Drive parent by itself. Use `01_Development/incoming` or `01_Development/projects` for skill/plugin/MCP source and product-development records, `01_Development/releases` for versioned release packages, `04_Library/tools` for reusable tools, `05_Docs` for reusable guides/prompts/architecture/decisions, `06_Platforms/<platform>` for platform-specific configuration and handoffs, `02_Workspace` for ordinary project workspaces, and `00_Registry` for repository/deployment/storage/migration records.
5. When a durable ChatGPT or Codex project is created, create or link its companion Cloud Workspace in the same workflow. Route an ordinary project to `02_Workspace/projects/<project-code>/`; route a reusable software product such as a skill, plugin, MCP server, or `xh-tuvan` to `01_Development/projects/<product-name>/`. Keep source in GitHub once a repository exists, releases in `01_Development/releases`, and installed runtime in the application-managed location. Record the native project ID or URL and the Drive folder ID in `project.json`. Do not create a workspace for a transient chat or short task.
6. Check whether the requested storage connector, skill installer, repository, or deployment capability is actually available. Seeing source files does not mean a skill or plugin is installed. For updates, distinguish the source or release package from the installed runtime: confirm the actual installed copy after applying changes, otherwise report that only the source/release was updated and installation remains pending. Runtime installation may legitimately use an application-managed local path rather than Drive; record the source/release path and installed runtime path separately, and never treat a Drive copy as installed merely because it exists there.
7. Preserve existing files and history. Do not overwrite, move, rename, migrate, archive, or delete material unless the request authorizes it and the target has been verified.
8. Create only the folders needed for the task. Record identifiers, versions, revisions, source links, and hashes when the policy requires them.
9. Save through the supported durable mechanism. Treat executor scratch space as temporary, and never claim that a scratch link has been synchronized to Drive.
10. At handoff, state the canonical artifact, its effective version or revision, its destination, and any unsynchronized or unresolved item.

## Precedence and scope

- Follow system, developer, product, permission, and security instructions before this skill.
- Treat the AI_Space policy as authoritative for storage organization after those higher-priority constraints.
- Keep shared business rules and content independent of Claude or ChatGPT. Put only platform-specific adapters and instructions under the corresponding platform area.
- Use the applicable specialist skill as well as this governance skill. For example, use the skill creator for skills, the plugin creator for plugins, and the document skill for DOCX files.
- If a live repository, installed skill, running plugin, or existing workspace has a verified contract that conflicts with the target layout, stop the migration, preserve the current contract, and report the required compatibility work.

## Trigger examples

Apply this skill to requests such as:

- "Tạo một skill mới và lưu để lần sau dùng tiếp."
- "Đóng gói plugin này và đưa source lên GitHub."
- "Xuất báo cáo Word và tạo bản XHedited để tôi sửa."
- "Tài liệu hướng dẫn này nên lưu ở đâu?"
- "Tạo workspace cho báo cáo NCKT mới."
- "Di chuyển file Claude và ChatGPT về cấu trúc dùng chung."

Do not apply it merely because the conversation mentions a file while the user only asks for a short explanation and no file operation or durable deliverable is involved.
