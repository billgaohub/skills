# AIUCE Skill Library

A curated collection of AI agent skills for structured audit, multi-phase execution, and quality-assured workflows.

---

## Skills

### 1. 3phase-Audit — Three-Phase Structured Review

**File:** `3phase-audit.md`

A rigorous, adversarial audit protocol that forces completeness through three mandatory phases. Designed for code reviews, document audits, system design reviews, and critical decisions.

#### Core Philosophy

Most reviews are superficial — they find obvious issues but miss structural weaknesses and hidden assumptions. The three-phase protocol solves this by forcing adversarial thinking, mandatory reconstruction, and reusable knowledge distillation.

#### Three Phases

| Phase | Role | Objective |
|-------|------|-----------|
| **Phase 1: Adversary** | ⚔️ Critic | Destroy structural stability — find every way it can break |
| **Phase 2: Builder** | 🤝 Repair | Make it actually work — fix, refactor, generate tests |
| **Phase 3: Teacher** | 🎓 Distill | Extract reusable patterns — persist lessons to memory |

#### Invocation

```
AUDIT/3PHASE/
Target: <code | document | system-design | decision>
Constraint (optional): <performance | security | maintainability>
Depth (optional): <brief | standard | deep>
```

#### Trigger Keywords

```
audit, review, critic, 3phase, three-phase audit, code review, security review, find bugs, adversarial review
```

#### Example Usage

**Code Review:**
```
AUDIT/3PHASE/
Target: src/auth/login.py
Constraint: security
Depth: deep
```

**System Design:**
```
AUDIT/3PHASE/
Target: Microservice migration plan
Constraint: maintainability
Depth: standard
```

**Critical Decision:**
```
AUDIT/3PHASE/
Target: "Should we use GraphQL or REST for the new API?"
Depth: standard
```

#### Output Format

Each phase produces structured output:

- **[CRITIC]** — Fatal issues, high-risk issues, structural weaknesses, strongest counterexample, patch directions
- **[BUILDER]** — Refactor plan, fixed code, test cases (unit/boundary/stress/counterexample), remaining uncertainties
- **[TEACHER]** — Core reusable principles, failure pattern library, transferable templates

#### Verification Criteria

| Phase | Pass Condition |
|-------|---------------|
| Phase 1 | At least 1 fatal or high-risk issue found |
| Phase 2 | Test cases cover all Phase 1 counterexamples |
| Phase 3 | Experience persisted to memory system |

---

### 2. Task-Phase-Executor — Multi-Phase Task Execution with Dual-Perspective Audit

**File:** `task-phase-executor.md`

An automated multi-phase task executor that forces quality gates after every phase. Each phase runs: execute → report → dual-perspective audit → converge → fix → consensus.

#### Core Philosophy

Most task execution is fire-and-forget — run commands, done. There's no quality gate, no reflection, no learning. This skill solves this with a standardized execution loop and mandatory sub-agent adversarial audit after each phase.

#### Execution Flow

```
Phase 0 Execute → Report → Dual Audit → Converge → Fix → Consensus → Evaluate Phase 1
    ↓
Phase 1 Execute → ... →
    ↓
Phase N Execute → ... →
    ↓
Full Pipeline Summary Report
```

#### Per-Phase Execution Loop

1. **Execute Tasks** — Run all tasks, record execution process and problems
2. **Phase Execution Report** — Save to `reports/execution/phase-{N}-execution-report.md`
3. **Dual-Perspective Audit** — Launch two sub-agents: Executor Defense (80-95/100) vs Independent Auditor (30-55/100)
4. **Converge Disputes** — Executor-acknowledged problems → fix list; false positives → record; disagreements → flag manual
5. **Fix Problems** — Fatal/high-risk/structural immediately; minor → debt list
6. **Consensus Report** — Save to `reports/execution/phase-{N}-consensus-report.md`
7. **Evaluate Next Phase** — Modify plan if critical omissions, design defects, or security risks found

#### Invocation

**Method A — From file:**
```
execute plan: reports/my-plan.md
```

**Method B — Direct paste:**
```
execute plan:
## Phase 0: Environment Setup
- Task 1: Create directory
- Task 2: Install dependencies

## Phase 1: Core Implementation
- Task 1: ...
```

**Method C — Explicit command:**
```
/skill task-phase-executor reports/my-plan.md
```

#### Graduation Rules (Mandatory After Each Phase)

| # | Step | Output |
|---|------|--------|
| 1 | Execute tasks | Actual file/code changes |
| 2 | Execution report | `phase-{N}-execution-report.md` |
| 3 | Dual-perspective audit | Executor + Auditor outputs |
| 4 | Converge disputes | Dispute list clearly recorded |
| 5 | Fix problems | Verified fixes |
| 6 | Consensus report | `phase-{N}-consensus-report.md` |
| 7 | Evaluate next Phase | Modification decision stated |

#### Example: Simple Task Plan

```
execute plan:
## Phase 0: Setup
- Task 1: Create project directory
- Task 2: Initialize git

## Phase 1: Implementation
- Task 1: Write main.py
- Task 2: Write tests
```

#### Example: Complex System Migration

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

## Dual-Perspective Audit Explained

The core innovation of Task-Phase-Executor is the dual-perspective audit after every phase:

- **Executor Defense (Perspective A):** Proves all tasks completed correctly, provides evidence, rebuts auditor challenges. Self-score: 80-95/100.
- **Independent Auditor (Perspective B):** Finds all problems, classifies by severity (fatal/high-risk/structural/minor). Score: 30-55/100.

The gap between these two scores drives learning. Over time, the executor learns to catch what auditors catch, closing the quality loop.

---

## License

MIT