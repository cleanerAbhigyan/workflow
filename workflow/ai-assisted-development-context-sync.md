# Agent-assisted development and context-sync workflow

**Status:** In use for the RBI mock app; repeatable process documented for the independent predictor. **Partially automated, not a live Notion ↔ ChatGPT ↔ GitHub synchronization.**  
**Captured:** 2026-11-07  
**Trigger:** Manual development request / ChatGPT-to-VS-Code agent handoff

## Goal

Use **Notion + ChatGPT + VS Code coding agent + GitHub/GitHub Actions** to carry forward long-running technical projects with less repetitive context setting. Each milestone should leave reviewable source code, tests, logs, decisions, and links for the next session.

## Roles and sources of truth

| Component | Role | Automatic? |
| --- | --- | --- |
| **Notion** | Requirements, scope, research, decisions, study/project status | Updated only by an authorized user/agent action; no live sync |
| **ChatGPT** | Read current Notion and GitHub state, prepare scoped agent prompts, review evidence, coordinate updates | Only when explicitly invoked |
| **VS Code + coding agent** | Inspect local repository, implement scoped changes, run tests, update documentation, commit/push when configured/authorized | Assisted execution, requires invocation and access |
| **GitHub** | Canonical committed implementation, PR discussions, history and source documentation | Receives agent pushes |
| **GitHub Actions** | Run configured checks on push and PR | Automatic for the mock app where CI is configured |

## Repeatable milestone loop

1. **Orient in Notion.** Read the current project brief, constraints, linked research and decisions. Do not treat plans as completed implementation.
2. **Inspect actual GitHub state.** Check the correct remote/repository, default and feature branches, open/merged PRs, current commits, current docs and CI. Resolve conflicts with stale Notion notes before making a change.
3. **Prepare the scoped implementation instruction in ChatGPT.** Specify outcome, acceptance criteria, repo, branch rules, tests, exclusions and evidence required. Hand off to the VS Code coding agent.
4. **Agent preflight in VS Code.** Read `README.md`, `AGENTS.md`, `docs/PROJECT_CONTEXT.md`, `docs/ROADMAP.md` and `docs/DEVELOPMENT_LOG.md` as present. Run `git status -sb`, `git remote -v` and `git branch --show-current`. Integrate upstream safely, never clobber uncommitted changes.
5. **Implement and validate.** Archive a sanitized prompt in `docs/prompts/YYYY-MM-DD-short-task.md`; change only scoped code; add/update tests. For the mock app, relevant checks include `npm run lint`, `npm run typecheck`, `npm run format:check`, `npm test`, `npm run build` and, for browser flows, `npm run test:e2e`. Use project-specific checks for the predictor after implementation exists.
6. **Preserve context.** Update README, project context, roadmap, development log, architecture/data contracts as appropriate, reflecting *actual* implementation and unresolved gaps. Commit source + tests + sanitized prompt + documentation together.
7. **Push and confirm.** Push to the **correct repository and agreed branch** without force-push. GitHub Actions runs configured checks. Review the remote SHA, latest PR state and relevant CI result; report what passed, failed or was not run.
8. **Reconcile in ChatGPT and Notion.** Review current GitHub evidence against the original requirements. Update the existing Notion project record only when requested/authorized, recording verified milestone, commit/PR reference, actual tests, decisions and next steps. No automatic success or completion inference.
9. **Resume later.** At the next session, reread current Notion and live GitHub state instead of relying solely on chat memory.

## Two implementations of the same process

### RBI mock app — active example

- **Notion source:** [Exam Experience App](https://app.notion.com/p/410504b1d5b68152b201dc8f784e3468)
- **GitHub:** [cleanerAbhigyan/rbi-mock-app](https://github.com/cleanerAbhigyan/rbi-mock-app)
- **Local folder:** `~/projects/rbi-app/rbi-mock-app`
- **Evidence:** `AGENTS.md`, `docs/PROJECT_CONTEXT.md`, `docs/ROADMAP.md` and the GitHub PR history document the agent loop, tests and CI. Phases 0, 1A and 1B include a separately labeled custom demo/timed-practice implementation; the verified real-PYQ catalog is still empty in the current docs.
- **Important live-state discrepancy discovered 2026-11-07:** [PR #1](https://github.com/cleanerAbhigyan/rbi-mock-app/pull/1) was **merged** on 2026-11-07 at 17:09 UTC. Some Notion and GitHub instructions still say to keep the feature branch and PR open and not merge. Those instructions are now stale. **Reconcile the post-merge branching and review policy before the next implementation milestone; do not assume PR #1 remains active.**
- **CI:** The mock app repository documents GitHub Actions for lint, types, format, unit tests, build and browser journeys.

### RBI predictor — planned application

- **Notion source:** [LLM PYQ Prediction](https://app.notion.com/p/410504b1d5b681f98f3aca13b0612ebf)
- **GitHub:** [cleanerAbhigyan/question-predictor](https://github.com/cleanerAbhigyan/question-predictor)
- **Local folder:** `~/projects/rbi-app/question-predictor`
- **Evidence:** `README.md` and `AGENTS.md` define a similar prompt → implement → test → document → commit → push → review workflow, but the repository describes the predictor as a future research/model-development project. **Do not treat its model, dataset, backtests, feature branch or CI as completed based on the plan.**
- **Branch policy:** Before first actual development, inspect the live branch/PR state; the earlier Notion plan proposes a long-lived feature branch and PR for predictor milestones, with merge requiring explicit approval.

These are independent repositories. No monorepo or premature cross-repo runtime dependency. A future model-to-app transfer needs a versioned, validated, human-approved question contract and accurate source labeling.

## What's automated versus manual

**Already automated where configured:** GitHub Actions CI on mock-app pushes/PRs; repeatable agent instructions and project docs help an invoked VS Code agent execute routine implementation steps.

**Still manual or approval-gated:** Starting/authorizing new work, ChatGPT↔VS Code handoff, evaluating scope and code quality, verifying actual GitHub PR/CI state, resolving merge decisions, updating Notion, and any GitHub↔Notion record synchronization. No unattended coding loop or real-time three-way mirror was established.

## Risks / safeguards

- **Stale context:** Always prefer live PR/branch/commit/CI evidence when notes disagree; explicitly reconcile.
- **No false completion:** A successful build does not mean the whole product is shipped; planned predictor experiments are not verified results.
- **Separate sources:** Verified PYQs, reconstructions, developer fixtures and model-generated practice must be distinguishable.
- **Security:** Never save secrets in prompts, docs, commits or public repositories; avoid personal attempt histories and non-redistributable source papers.
- **Safe Git discipline:** Never force push or erase local changes. Don't merge without agreed review policy.

## Next improvements (proposals only — not implemented)

1. Define a normalized milestone event with repo, branch, commit SHA, PR state, CI conclusion, timestamp, impacted Notion record and verified summary.
2. Add an authorized GitHub Actions or webhook → Notion API integration that updates the **existing** workflow/project record after an evidence check; initially prefer a draft/review queue to prevent false status updates.
3. Add stale-reference alerts when Notion branch/PR guidance contradicts live GitHub state.
4. Introduce a reusable VS Code agent handoff template and milestone checklist; keep approvals for merges, permissions, secrets and production changes.

## Original sources

- [RBI Grade B — development architecture](https://app.notion.com/p/3ff504b1d5b680eeb770c3395de0fdde)
- [Mock app specification](https://app.notion.com/p/410504b1d5b68152b201dc8f784e3468)
- [Predictor specification](https://app.notion.com/p/410504b1d5b681f98f3aca13b0612ebf)
- [Mock app AGENTS.md](https://github.com/cleanerAbhigyan/rbi-mock-app/blob/main/AGENTS.md)
- [Mock app context](https://github.com/cleanerAbhigyan/rbi-mock-app/blob/main/docs/PROJECT_CONTEXT.md)
- [Predictor AGENTS.md](https://github.com/cleanerAbhigyan/question-predictor/blob/main/AGENTS.md)
