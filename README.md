# workflow

A version-controlled home for reusable automations, integrations, data and AI workflows.

**Notion tracking hub:** [workflow — My Mind](https://app.notion.com/p/411504b1d5b681d2b02fdda09be680e8)

## Source of truth

- **GitHub:** source code, example configurations, tests, execution instructions and version history.
- **Notion:** Workflow Registry, business purpose, progress, key decisions, problems, lessons and next steps.

Each new workflow should have a Notion Registry entry and a matching file or directory under `workflow/`. Cross-link both records.

## Captured workflow

- **[AI-assisted development & context sync](workflow/ai-assisted-development-context-sync.md)** — repeatable Notion → ChatGPT → VS Code agent → GitHub/CI → reviewed Notion-update loop, used for RBI mock app development and planned for the independent RBI predictor. [Notion Registry record](https://app.notion.com/p/411504b1d5b6818c82d6dfa34cfb4bb6). Agent-assisted / partially automated; not a live two-way sync.

## Suggested layout

```text
workflow/
  <workflow-name>.md          # Process overview, sources, decisions, automation gaps
  <workflow-name>/
    README.md                 # Goal, trigger, inputs, outputs, setup and execution
    src/                      # Workflow implementation where applicable
    tests/                    # Validation where applicable
    config.example.*          # Non-secret configuration examples
```

Create code directories only when an actual implementation exists. Do not store API keys, passwords, private tokens or secrets in commits.

## Per-workflow documentation

Include its goal, trigger, inputs/outputs, tools and dependencies, steps to execute and verify it, error handling, run evidence, known issues, and a link to its Notion record.

## Sync status

This repository and the Notion page are linked for navigation. **Automatic two-way synchronization has not been configured.** Updating a GitHub file does not automatically update the Notion tracker, and vice versa.
