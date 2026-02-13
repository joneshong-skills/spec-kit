---
name: spec-kit
description: >-
  Guide spec-driven development (SDD) workflow. This skill should be used when
  the user asks to "write a spec", "create a specification", "spec-driven
  development", "build a feature spec", "generate implementation plan",
  "break down tasks from spec", "規格文件", "撰寫規格", "spec 文件",
  "技術規格", "產品規格", "寫規格", "建立規格", "SDD", "spec-kit",
  mentions specification-driven development, or discusses creating structured
  feature specifications, implementation plans, task breakdowns, or project
  constitutions for software projects.
version: 0.1.0
tools: Read, Bash, Edit, Write, Glob, Grep
argument-hint: "<feature description or SDD command>"
---

# Spec Kit -- Spec-Driven Development Toolkit

Implement the Spec-Driven Development (SDD) methodology: specifications drive code,
not the other way around. Transform feature descriptions into structured specs,
implementation plans, and executable task lists.

## Core Concept

SDD inverts the traditional power structure: specifications are the primary artifact,
code is generated from them. The workflow is:

1. **Specify** -- Define WHAT and WHY (no tech stack)
2. **Clarify** -- Resolve ambiguities interactively
3. **Plan** -- Generate technical implementation plan
4. **Tasks** -- Break plan into executable, dependency-ordered tasks
5. **Analyze** -- Cross-artifact consistency check
6. **Implement** -- Execute tasks phase by phase

## Prerequisites

Ensure the project has been initialized with Spec Kit (`specify init`). If not,
guide the user to set up the `.specify/` directory structure with templates and scripts.
See `references/quickstart.md` for installation instructions.

If the project lacks `.specify/`, create the necessary structure manually:
- `specs/` directory at project root for feature specifications
- `memory/constitution.md` for project principles (use `references/constitution-template.md`)

## Workflow Commands

Each command maps to a specific phase. Read the corresponding command reference
in `references/commands/` for the full execution protocol.

### 1. Specify (`/spec-kit specify <description>`)

Create a feature specification from a natural language description.

Execution protocol: Read `references/commands/specify.md` for the full workflow.

Key steps:
1. Generate a concise branch name from the description
2. Determine next feature number by scanning existing specs/branches
3. Create branch and `specs/[NNN-feature-name]/spec.md`
4. Fill the spec template (`references/spec-template.md`) focusing on:
   - User scenarios with prioritized stories (P1, P2, P3)
   - Functional requirements (testable, unambiguous)
   - Success criteria (measurable, technology-agnostic)
5. Validate spec quality with a requirements checklist
6. Present max 3 clarification questions for ambiguous items

Rules:
- Focus on WHAT users need and WHY -- no implementation details
- Mark genuinely unclear items with `[NEEDS CLARIFICATION]` (max 3)
- Make informed guesses for everything else based on domain conventions

### 2. Clarify (`/spec-kit clarify [focus area]`)

Identify and resolve spec ambiguities through targeted questions.

Execution protocol: Read `references/commands/clarify.md` for the full workflow.

Key steps:
1. Load current spec and scan for ambiguities across taxonomy categories
2. Generate max 5 prioritized questions (one at a time, sequential)
3. Each question: provide a recommended option with reasoning
4. After each answer: immediately update spec inline and save
5. Report sections touched and coverage summary

Rules:
- Max 5 questions per session, 10 across all sessions
- Each question must be answerable with short answer or multiple choice
- Integrate answers directly into appropriate spec sections
- Never reveal upcoming questions in advance

### 3. Plan (`/spec-kit plan <tech stack>`)

Generate an implementation plan from the specification.

Execution protocol: Read `references/commands/plan.md` for the full workflow.

Key steps:
1. Load feature spec and project constitution
2. Fill Technical Context with stack details
3. Run Constitution Check gates
4. Phase 0: Research unknowns, generate `research.md`
5. Phase 1: Generate `data-model.md`, `contracts/`, `quickstart.md`
6. Report generated artifacts

Uses template: `references/plan-template.md`

### 4. Tasks (`/spec-kit tasks`)

Generate an actionable, dependency-ordered task list.

Execution protocol: Read `references/commands/tasks.md` for the full workflow.

Key steps:
1. Load plan.md (required) and spec.md (for user story priorities)
2. Optionally load data-model.md, contracts/, research.md
3. Organize tasks by user story for independent implementation
4. Generate `tasks.md` with phases: Setup, Foundational, User Stories (by priority), Polish

Task format: `- [ ] [TaskID] [P?] [Story?] Description with file path`

Uses template: `references/tasks-template.md`

### 5. Analyze (`/spec-kit analyze`)

Non-destructive cross-artifact consistency analysis.

Execution protocol: Read `references/commands/analyze.md` for the full workflow.

Key steps:
1. Load spec.md, plan.md, tasks.md (all required)
2. Build semantic models and run detection passes:
   - Duplication, ambiguity, underspecification
   - Constitution alignment, coverage gaps, inconsistency
3. Produce analysis report with severity-ranked findings
4. Recommend next actions

Rules: STRICTLY READ-ONLY. Never modify files.

### 6. Implement (`/spec-kit implement`)

Execute the implementation plan task by task.

Execution protocol: Read `references/commands/implement.md` for the full workflow.

Key steps:
1. Check all checklists in `checklists/` directory -- halt if incomplete
2. Load tasks.md and all design documents
3. Set up project structure and ignore files
4. Execute tasks phase by phase respecting dependency order
5. Mark completed tasks as `[X]` in tasks.md

### 7. Constitution (`/spec-kit constitution <principles>`)

Create or update the project constitution with architectural principles.

Execution protocol: Read `references/commands/constitution.md` for the full workflow.

Uses template: `references/constitution-template.md`

### 8. Checklist (`/spec-kit checklist <domain>`)

Generate requirements quality checklists ("unit tests for English").

Execution protocol: Read `references/commands/checklist.md` for the full workflow.

Key concept: Checklists test whether REQUIREMENTS are well-written, not whether
the implementation works. Ask "Is X clearly specified?" not "Does X work?"

### 9. Tasks to Issues (`/spec-kit taskstoissues`)

Convert tasks.md into GitHub Issues.

Execution protocol: Read `references/commands/taskstoissues.md` for the full workflow.

## Template Reference

All templates live in `references/`:
- **`spec-template.md`** -- Feature specification structure
- **`plan-template.md`** -- Implementation plan structure
- **`tasks-template.md`** -- Task list structure with phases
- **`constitution-template.md`** -- Project constitution structure
- **`checklist-template.md`** -- Checklist structure
- **`agent-file-template.md`** -- Agent context file structure

## SDD Methodology Reference

For the full philosophical foundation and methodology rationale, read
`references/spec-driven.md`. Key principles:

- Specifications are the lingua franca; code is their expression
- Executable specifications eliminate the intent-implementation gap
- Continuous refinement over one-time gates
- Research-driven context gathering
- Bidirectional feedback from production to specs

## Quick Reference

| Phase | Input | Output | Template |
|-------|-------|--------|----------|
| Specify | Feature description | `spec.md` | spec-template.md |
| Clarify | spec.md + questions | Updated spec.md | -- |
| Plan | spec.md + tech stack | plan.md, research.md, data-model.md, contracts/ | plan-template.md |
| Tasks | plan.md + spec.md | tasks.md | tasks-template.md |
| Analyze | spec + plan + tasks | Analysis report | -- |
| Implement | tasks.md + all docs | Working code | -- |
| Constitution | Principles | constitution.md | constitution-template.md |
| Checklist | Domain focus | checklists/*.md | checklist-template.md |

## Continuous Improvement

This skill evolves with each use. After every invocation:

1. **Reflect** — Identify what worked, what caused friction, and any unexpected issues
2. **Record** — Append a concise lesson to `lessons.md` in this skill's directory
3. **Refine** — When a pattern recurs (2+ times), update SKILL.md directly

### lessons.md Entry Format

```
### YYYY-MM-DD — Brief title
- **Friction**: What went wrong or was suboptimal
- **Fix**: How it was resolved
- **Rule**: Generalizable takeaway for future invocations
```

Accumulated lessons signal when to run `/skill-optimizer` for a deeper structural review.
