# Start Here — Unified Project Starter Kit v3.3

This project system merges three useful layers:

1. **Project control** from Project Starter Kit v2: phase gates, vertical slices, approval before changes, tracking, and GitHub discipline.
2. **AI engineering memory** from the new workflow: one problem per chat, clean extracted files, checkpoints, reusable prompts, reusable patterns, and context resets.
3. **Service/API design discipline** from the added documents: explicit API surface, data model, security design, failure scenarios, scaling strategy, and observability before implementation.

The result is a controlled AI-assisted engineering workflow.

```text
AI chat = temporary reasoning
Project files = permanent source of truth
/ai files = reusable AI engineering memory
Service design files = pre-implementation architecture control
Commits = proof of work
```

---

## The Hard Rule

Do not let important work live only in chat.

Every meaningful AI-assisted work session must produce one durable output:

| Work Type | Durable Output |
|---|---|
| Project idea | `PROJECT_BRIEF.md` |
| Current state | `STATUS.md` |
| Active plan | `PLAN.md` or `plans/YYYY-MM-DD_slice_name.md` |
| Architecture decision | `docs/ARCHITECTURE.md` and `DECISION_LOG.md` |
| Service/API design | `ai/sessions/designs/YYYY-MM-DD_service_name_api_design.md` |
| Generic design session | `ai/sessions/designs/YYYY-MM-DD_design_name.md` |
| Feature build | `ai/sessions/features/YYYY-MM-DD_feature_name.md` |
| Bug investigation | `ai/sessions/debug/YYYY-MM-DD_issue_name.md` |
| Messy or long chat | `ai/checkpoints/YYYY-MM-DD_checkpoint_name.md` |
| Reusable lesson | `ai/patterns/pattern_name.md` |
| Reusable instruction | `ai/prompts/prompt_name.md` |
| Completed slice | `SLICE_REVIEWS.md`, `PROGRESS_NOTE.md`, `COMMIT_NOTES.md` |

---

## What Belongs Where

### Root project files

Root files are the operational source of truth.

Use them to answer:

- What is this project?
- What phase are we in?
- What is the next action?
- What is approved?
- What changed?
- What is ready to commit?

Core root files:

```text
README.md
PROJECT_BRIEF.md
CONTEXT.md
STATUS.md
PLAN.md
PHASE_GATES.md
BACKLOG.md
ROADMAP.md
DECISION_LOG.md
SLICE_REVIEWS.md
LESSONS_LEARNED.md
CHANGELOG.md
RELEASE_NOTES.md
COMMIT_NOTES.md
PROGRESS_NOTE.md
PROGRESS_NOTES.md
CLAUDE.md
AGENTS.md
```

### `docs/`

`docs/` contains stable technical documentation.

Use it for approved architecture, security, testing, API, data model, performance, workflow, and versioning.

Do not dump raw AI session notes into `docs/`. Promote only clean, approved conclusions.

### `plans/`

`plans/` contains approved or proposed slice plans.

Use `PLAN.md` for the active plan. Use dated files in `plans/` for larger or historical task plans.

### `ai/`

`ai/` contains AI working memory and reusable AI system files.

This is not a replacement for project docs. It is the bridge between temporary AI conversations and permanent project knowledge.

---

## Default Workflow

### Phase 0 — Initialize the project

Use this phase only to create the control structure.

Create or confirm:

```text
PROJECT_BRIEF.md
CONTEXT.md
STATUS.md
PLAN.md
PHASE_GATES.md
BACKLOG.md
CLAUDE.md
AGENTS.md
ai/README.md
ai/templates/
```

---

### Phase 1 — Plan the smallest useful slice

Phase 1 decides what should happen. Do not edit implementation files during Phase 1.

Phase 1 must answer:

1. What are we trying to prove?
2. What is the smallest useful vertical slice?
3. What is explicitly out of scope?
4. What files are expected to change?
5. What checks will run first?
6. How will success be verified?
7. What risks remain?
8. Is Phase 2 approved?

---

### Phase 2 — Implement only the approved slice

Required loop:

```text
check → fix → verify → commit → push
```

Rules:

- Run the initial check first.
- Change only approved files.
- Do not add unrelated features.
- Do not refactor unrelated code.
- Do not fake verification.
- Update tracking files before commit.

---

### Phase 3 — Review, checkpoint, and promote knowledge

After the slice is complete, extract the value.

1. Review the slice against success criteria.
2. Checkpoint the clean current state for future AI sessions.
3. Promote reusable lessons into patterns or prompts.

---

## Approval Rule

Before any agent changes files, it must show:

1. current phase
2. current goal
3. exact files it wants to change
4. reason each file must change
5. smallest safe change
6. risks
7. check command before changes
8. verification after changes
9. rollback plan
10. approval request

---

## Sub-Agent Workflow

This repo includes Claude Code sub-agents in `.claude/agents/`.

Use them as controlled specialists, not autonomous project owners:

```text
repo-cartographer → project-steward → slice-planner
→ implementation
→ test-verifier
→ security-reviewer if needed
→ docs-promoter
```

Read `ai/agents/AGENT_ROSTER.md`, `ai/agents/AGENT_USAGE_RULES.md`, and `ai/agents/AGENT_REVIEW_GATES.md`.

---

## Final Mental Model

```text
Project control files tell the agent what is true.
AI session files preserve what the agent figured out.
Checkpoints reset the agent without losing the plot.
Patterns and prompts turn repeated work into reusable leverage.
Commits prove the work actually changed.
```
