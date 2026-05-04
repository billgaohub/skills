---
name: task-phase-executor
description: >
  Multi-phase task executor — input an implementation plan, automatically execute all Phases with dual-perspective audit.
  After each Phase: execution report → sub-agent audit → converge → fix → consensus.
  Supports natural language and explicit command invocation.
version: 1.0.0
author: Bill
license: MIT
category: workflow
tags: [execution, multi-phase, audit, workflow, automation, plan-execution]
trigger_keywords:
  - execute plan
  - run plan
  - multi-phase
  - phase execution
  - task executor
  - implementation plan
  - run task
---

# Task-Phase-Executor — Multi-Phase Task Execution with Dual-Perspective Audit

A workflow skill that takes an implementation plan (with Phases 0/1/2/.../N) and executes it automatically, with mandatory dual-perspective audit after each Phase to ensure quality.

## Why This Skill?

Most task execution is fire-and-forget — run commands, done. There's no quality gate, no reflection, no learning. This skill solves that by:

1. **Standardized execution loop** — every Phase gets: execute → report → audit → converge → fix → consensus
2. **Forced quality gate** — sub-agent dual-perspective audit (executor vs auditor) catches what you miss alone
3. **Automatic adaptation** — audit findings can modify the next Phase's plan without manual intervention

## Input Format

**Method A: File path**
```
execute plan: reports/my-plan.md
```

**Method B: Direct paste**
```
execute plan:
## Phase 0: Environment Setup
- Task 1: Create directory
- Task 2: Install dependencies

## Phase 1: Core Implementation
- Task 1: ...
```

**Method C: Explicit command**
```
/skill task-phase-executor reports/my-plan.md
```

---

## Execution Flow

```
Phase 0 Execute → Report → Dual Audit → Converge → Fix → Consensus → Evaluate Phase 1
    ↓
Phase 1 Execute → ... →
    ↓
Phase N Execute → ... →
    ↓
Full Pipeline Summary Report
```

---

## Per-Phase Execution Loop

### Step 1: Execute Tasks

Execute all tasks for the current Phase:
- Record each task's execution process
- When problems occur, record problem details and resolution
- Use terminal commands / file operations / code modifications to complete work

### Step 2: Output Phase Execution Report

Save to: `reports/execution/phase-{N}-execution-report.md`

Required structure:
```markdown
# Phase {N} Execution Report

**Time**: YYYY-MM-DD HH:MM
**Executor**: Agent ID

## Task Checklist
| # | Task | Status | Result |
|---|------|--------|--------|

## Detailed Execution Log
### Task 1: xxx
- Execution: ...
- Problem encountered: ...
- Resolution: ...
- Verification: ...

## Problem Summary
1. ...

## Incomplete Items
- ...
```

### Step 3: Sub-Agent Dual-Perspective Audit

**Launch two sub-agents for adversarial audit:**

**Perspective A (Executor Defense)**:
```
You are the executor perspective. Your task is:
1. Prove that all Phase N tasks were completed correctly
2. Provide evidence to rebut each audit challenge
3. Score: 80-95/100

After reading the execution report, output:
- Completion proof
- Evidence list
- Rebuttals to auditor challenges
```

**Perspective B (Independent Auditor)**:
```
You are the independent auditor perspective. Your task is:
1. Find all problems in Phase N execution
2. Classify by severity: fatal / high-risk / structural / minor
3. Score: 30-55/100

After reading the execution report, output:
- Problem list (classified)
- Strongest challenges
- Improvement suggestions
```

**Audit convergence**:
After both outputs, identify disputed points:
- Executor-acknowledged problems → add to fix list
- Auditor false positives → record but skip
- Disagreements → flag for manual decision

### Step 4: Fix Audit Findings

Fix by priority:

| Severity | Action |
|----------|--------|
| Fatal / High-risk | Fix immediately before next Phase |
| Structural weakness | Fix immediately |
| Affects next Phase | Fix immediately |
| Minor issues | Record to debt list, don't block |

### Step 5: Output Phase Consensus Report

Save to: `reports/execution/phase-{N}-consensus-report.md`

Required structure:
```markdown
# Phase {N} Consensus Report

**Audit Time**: YYYY-MM-DD HH:MM
**Participants**: Executor / Auditor

## Consensus Reached
- Completed and confirmed: ...
- Existing problems: ...
- Fixed problems: ...

## Disputed Points
- ...

## Debt List
| # | Problem | Severity | Status |
|---|---------|----------|--------|

## Scores
- Executor self-score: XX/100
- Auditor score: XX/100
- Consensus score: XX/100
```

### Step 6: Evaluate Next Phase Plan

Check if audit findings affect next Phase:

**Modify next Phase when:**
- Critical omissions found
- Design defects found
- Security risks found
- Dependencies that affect execution found

**Modification process**:
1. Update the plan file
2. Record reason for change
3. Continue execution (no manual approval needed)

**No modification needed**:
- Continue with original plan

---

## Graduation Rules (Must Follow)

After each Phase, ALL of the following must be completed — skipping any is a violation:

| # | Step | Output | Verification |
|---|------|--------|--------------|
| 1 | Execute tasks | Actual file/code changes | ls/diff verification |
| 2 | Execution report | `phase-{N}-execution-report.md` | File exists |
| 3 | Dual-perspective audit | Sub-agent outputs | Executor + Auditor views |
| 4 | Converge disputes | Dispute list | Clearly recorded |
| 5 | Fix problems | Actual fixes | Fix verification |
| 6 | Consensus report | `phase-{N}-consensus-report.md` | File exists |
| 7 | Evaluate next Phase | Modification decision | Clearly stated |

**Skipping any step is a violation.**

---

## Modification Thresholds

| Problem Type | Impact | Action |
|--------------|--------|--------|
| Critical omission | Missing key tasks | → Modify next Phase |
| Design defect | Architecture/logic error | → Modify next Phase |
| Security risk | Potential security issue | → Modify next Phase |
| Dependency break | Affects subsequent execution | → Modify next Phase |
| Minor issue | Quality issue | → Record debt, don't modify |

---

## Final Output

After all Phases complete, output full pipeline summary:

Save to: `reports/execution/full-pipeline-report.md`

Required structure:
```markdown
# Full Pipeline Report

**Plan**: {plan name}
**Execution time**: YYYY-MM-DD HH:MM ~ HH:MM
**Total Phases**: N

## Summary
- Successful Phases: X
- Modified Phases: Y
- Cumulative debt: Z

## Phase Details
### Phase 0
- Summary: ...
- Consensus score: XX/100
- Link: phase-0-consensus-report.md

### Phase 1
- ...

## Overall Scores
- Executor average: XX/100
- Auditor average: XX/100
- Final consensus: XX/100

## Debt Summary
| Phase | Problem | Severity | Status |
|-------|---------|----------|--------|

## Outstanding Items
- ...
```

---

## Sub-Agent Invocation

Use your agent's sub-agent system to launch the dual-perspective audit:

```python
# Method 1: Use sub-agent orchestration (preferred if available)
result = subagent_orchestrator.orchestrate(
    task="Audit Phase N execution results",
    agents=["executor_perspective", "auditor_perspective"],
    mode="parallel"
)

# Method 2: Use delegate_task (fallback)
result = delegate_task(
    goal="Audit Phase N execution from executor perspective",
    context=execution_report_content
)
```

For agents without sub-agent systems, you can simulate this by:
1. First thinking from the executor perspective (prove completion)
2. Then thinking from the auditor perspective (find problems)
3. Converging on the disputed points

---

## Adaptation Notes

To adapt this skill for your agent:

- **Output paths**: Replace `reports/execution/` with your agent's report storage location
- **Sub-agent system**: Replace `subagent_orchestrator.orchestrate()` with your agent's sub-agent capability
- **Trigger keywords**: Add to your agent's skill matching system
- **Manual decision flag**: The `disagreements → flag for manual decision` step requires a human-in-the-loop — ensure your agent can pause and ask for input

## Example Usage

### Simple Task Plan

```
execute plan:
## Phase 0: Setup
- Task 1: Create project directory
- Task 2: Initialize git

## Phase 1: Implementation
- Task 1: Write main.py
- Task 2: Write tests
```

### Complex System Migration

```
execute plan:
## Phase 0: Analysis
- Task 1: Audit existing system
- Task 2: Identify dependencies

## Phase 1: Design
- Task 1: Create migration plan
- Task 2: Risk assessment

## Phase 2: Implementation
- Task 1: Migrate data layer
- Task 2: Migrate business logic
- Task 3: Update tests

## Phase 3: Validation
- Task 1: Integration tests
- Task 2: Performance benchmarks
```

---

## License

MIT