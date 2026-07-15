> ⚠️ **Deprecated — legacy AIUCE family.** This repo is being consolidated into **SONUV** / **AIOBR** / a unified history archive (2026). No new work is accepted. Current status: **[aiuce.com](https://aiuce.com)**. _Marked 2026-07-15._
>
> _本仓库属旧 AIUCE 体系，正整合进 SONUV / AIOBR / 统一历史归档，不再接受新改动；最新状态见 aiuce.com。_
> **Disposition**: **Closed**
> **处置**：不再以 AIUCE 为母品牌维护；已归档只读。


# AIUCE Skill Library

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/billgaohub/skills)](https://github.com/billgaohub/skills/stargazers)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

A curated collection of AI agent skills for structured audit, multi-phase execution, and quality-assured workflows. This library powers the AIUCE (AI Utility & Capability Engine) framework with battle-tested protocols for adversarial review, task orchestration, and continuous improvement.

---

## 📁 Repository Structure

```
skills/
├── README.md              # This file
├── 3phase-audit.md        # Three-Phase Structured Audit Protocol
└── task-phase-executor.md # Multi-Phase Task Executor with Dual-Perspective Audit
```

---

## 🛠 Skills

### 1. 3phase-Audit — Three-Phase Structured Review

**File:** [`3phase-audit.md`](3phase-audit.md)

A rigorous, adversarial audit protocol that forces completeness through three mandatory phases. Designed for code reviews, document audits, system design reviews, and critical decisions.

#### Core Philosophy

Most reviews are superficial — they find obvious issues but miss structural weaknesses and hidden assumptions. The three-phase protocol solves this by forcing adversarial thinking, mandatory restructuring, and reusable knowledge distribution.

#### Three Phases

| Phase | Role | Objective | Output |
|-------|------|-----------|--------|
| **Phase 1: Adversary** | Critic | Destroy structural stability — find every way it can break | [CRITIC] — Fatal issues, high-risk issues, structural weaknesses, strongest counterexample, patch directions |
| **Phase 2: Builder** | Repair | Make it actually work — fix, refactor, generate tests | [BUILDER] — Refactor plan, fixed code, test cases (unit/boundary/stress/counterexample), remaining uncertainties |
| **Phase 3: Teacher** | Distill | Extract reusable patterns — persist lessons to memory | [TEACHER] — Core reusable principles, failure pattern library, transferrable templates |

#### Invocation

```
AUDIT/3PHASE/
Target: <code | document | system-design | decision>
Constraint (optional): <performance | security | maintainability>
Depth (optional): <brief | standard | deep>
```

#### Trigger Keywords

```
audit, review, critical, 3phase, three-phase audit, code review, security review, find bugs, adversarial review
```

#### Verification Criteria

| Phase | Pass Condition |
|-------|----------------|
| Phase 1 | At least 1 fatal or high-risk issue found |
| Phase 2 | Test cases cover all Phase 1 counterexamples |
| Phase 3 | Experience persisted to memory system |

---

### 2. Task-Phase-Executor — Multi-Phase Task Execution with Dual-Perspective Audit

**File:** [`task-phase-executor.md`](task-phase-executor.md)

An automated multi-phase task executor that forces quality gates after every phase. Each phase runs: execute → report → dual-perspective audit → converge → fix → consensus.

#### Core Philosophy

Most task execution is fire-and-forget — run commands, done. There is no quality gate, no reflection, no learning. This skill solves this with a standardized execution loop and mandatory sub-agent adversarial audit after each phase.

#### Execution Flow

```
Phase 0 Execute → Report → Dual Audit → Converge → Fix → Consensus → Evaluate Phase 1
    ↓
Phase 1 Execute → ... →
    ↓
Phase N Execute → ...
    ↓
Full Pipeline Summary Report
```

#### Per-Phase Execution Loop

1. **Execute Tasks** — Run all tasks, record execution process and problems
2. **Phase Execution Report** — Save to `reports/execution/phase-{N}-{date}-execution-report.md`
3. **Dual-Perspective Audit** — Launch two sub-agents: Executor Defenses (80-95/100) vs Independent Auditor (30-55/100)
4. **Converge Disputes** — Executor-acknowledged problems → fix list; false positives → record; disagreements → flag manual
5. **Fix Problems** — Fatal/high-risk/structural immediately; minor (debug) list
6. **Consensus Report** — Save to `reports/execution/phase-{N}-{date}-consensus-report.md`
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

#### Gradiation Rules (Mandatory After Each Phase)

| # | Step | Output |
|---|------|--------|
| 1 | Execute tasks | Actual file/code changes |
| 2 | Execution report | `phase-{N}-{date}-execution-report.md` |
| 3 | Dual-perspective audit | Executor + Auditor outputs |
| 4 | Converge disputes | Dispute list clearly recorded |
| 5 | Fix problems | Verified fixes |
| 6 | Consensus report | `phase-{N}-{date}-consensus-report.md` |
| 7 | Evaluate next phase | Modification decision stated |

---

## 📖 Usage Guide

### Prerequisites

These skills are designed for AI agents with tool execution capabilities (shell commands, file operations, API calls).

### Getting Started

1. **Audit a codebase:**
   ```
   AUDIT/3PHASE/
   Target: src/auth/login.py
   Constraint: security
   Depth: deep
   ```

2. **Execute a multi-phase plan:**
   ```
   execute plan:
   ## Phase 1: Setup
   - Task 1: Create project directory
   - Task 2: Initialize git
   ```

### Selecting the Right Skill

| Scenario | Skill |
|----------|-------|
| Code review, design audit, critical decision | **3phase-Audit** |
| Complex multi-step execution with quality gates | **Task-Phase-Executor** |
| Both: execute then audit | Run **Task-Phase-Executor**, then invoke **3phase-Audit** on outputs |

---

## 📄 License

MIT License — see individual skill files for details.

---

*Maintained by AIUCE. For questions, open an issue or submit a PR.*