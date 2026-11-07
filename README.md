# workflow

A version-controlled home for reusable automations, integrations, data and AI workflows.

**Notion tracking hub:** [workflow — My Mind](https://app.notion.com/p/411504b1d5b681d2b02fdda09be680e8)

## Source of truth

- **GitHub:** source code, example configurations, tests, execution instructions and version history.
- **Notion:** Workflow Registry, business purpose, progress, key decisions, problems, lessons and next steps.

Each new workflow should have a Notion Registry entry and a matching directory under `workflow/<workflow-name>/`. Cross-link both records.

## Suggested layout

```text
workflow/
  <workflow-name>/
    README.md         # Goal, trigger, inputs, outputs, setup and execution
    src/              # Workflow implementation
    tests/            # Validation
    config.example.*  # Non-secret configuration examples
```

Directories are created only as real workflows are added. Do not store API keys, passwords, private tokens or secrets in commits.

## Per-workflow documentation

Include its goal, trigger, inputs/outputs, tools and dependencies, steps to execute and verify it, error handling, run evidence, known issues, and a link to its Notion record.

## Sync status

This repository and the Notion page are linked for navigation. **Automatic two-way synchronization has not been configured.** Updating a GitHub file does not automatically update the Notion tracker, and vice versa.
