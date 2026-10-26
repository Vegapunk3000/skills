# Agents

This repository contains shareable agent skills.

## Rules

- Keep every skill portable across repositories and teammates.
- Do not hardcode local machine paths or Docsyde workspace-only paths in reusable skills.
- Put repo-specific behavior behind discovery: read local instructions, templates, and existing folders from the target repo.
- Validate changed skills before committing.
- If a skill bundles third-party content, preserve attribution and license notes.

## Workflow maintenance

- Honor the user's scope and prior authorization; read-only requests include
  memory and generated artifacts. Do not add permission gates for routine work.
- Keep route, review, artifact, and cleanup rules consistent across SKILL.md,
  referenced templates, worker instructions, and UI prompts.
- Use the repository validator for its supported versioned frontmatter.

## Validation

Use:

```powershell
.\scripts\validate-skills.ps1
npx skills add . --list
```

## Install Testing

Use local install tests before telling the team to update:

```powershell
npx skills add . --skill plan-it --agent <agent-name>
npx skills add . --skill plan-it --agent claude-code
```

## Cursor Cloud specific instructions

Cloud Agents run on Linux. Validate from the repository root with:

```bash
pwsh -NoLogo -File ./scripts/validate-skills.ps1
npx skills add . --list
```

PowerShell 7 comes from the environment install. The Skills CLI needs Node.js 22.20 or newer.

`npx skills add` and `scripts/install-local.ps1` write agent skill folders and `skills-lock.json` into the current directory. This repository does not ignore those files. Run install checks from a temporary directory so the skills tree stays unchanged:

```bash
repo="$(pwd)"
cd "$(mktemp -d)"
pwsh -NoLogo -File "$repo/scripts/install-local.ps1" -Skills plan-it -Agents claude-code -Yes
```
