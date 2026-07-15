# Repository Guidelines

## Project Structure & Module Organization

This repository is a Markdown-based personal agenda, not a software application. Keep task files in `Pendentes/` until completed, then move them to `Concluídos/` without renaming. Store one project description per file in `Projetos/<projeto>.md`. Project files may also define a default priority band for related tasks. Use `AI/` for human-facing documentation about the agenda workflow.

Codex skills live in `.agents/skills/`. Each skill has a `SKILL.md` and optional `agents/openai.yaml`. Current responsibilities are separated into `criar-tarefa`, `buscar-tarefas`, `agendar-notificacoes`, and `gerenciar-tarefas`; preserve those boundaries when editing them.

## Task Format & Naming

Name task files with lowercase, unaccented words separated by underscores:

```text
projeto_nome_da_tarefa_dd-mm-aaaa.md
nome_da_tarefa_SD.md
```

The date in the filename is the deadline, not the creation date. Every task begins with YAML metadata for `projeto`, `prazo`, `horario`, `criada_em`, `prioridade`, and `status`. Use `SD` for an unknown deadline or time. Keep descriptions brief and in natural language.

Allowed priorities are `não definida`, `baixa`, `média`, `alta`, and `urgente`. Keep non-completed statuses in `Pendentes/`; a `concluída` task belongs in `Concluídos/`.

## Development & Validation

There is no build, test, linter, or runtime service. Validate every changed skill before handoff:

```powershell
python -X utf8 <path-to-quick_validate.py> .agents\skills\<skill-name>
```

Use `git status --short` to confirm the intended files. Do not add generated caches, local credentials, or unrelated files.

## Change, Commit & Pull Request Guidelines

The repository has no commit history yet, so there is no established message convention. Use concise Conventional Commit-style messages, such as `feat: add task scheduling skill` or `docs: clarify task metadata`.

Keep each change focused. In a pull request, explain the behavior changed, list affected folders or skills, and include the validation command and result. For changes to task semantics or automation, give one natural-language example that demonstrates the intended behavior.

## Agent-Specific Instructions

Prefer filename filtering, then metadata headers, and read task descriptions only when required. Never overwrite a task on name collision. Before creating, updating, or cancelling reminders, inspect existing automations and avoid duplicates; never cancel the daily agenda review while managing an individual task.
