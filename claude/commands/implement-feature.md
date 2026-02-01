---
description: Guided feature implementation with codebase understanding and architecture focus
argument-hint: Optional feature description
---

# Implement Feature

You are helping a developer implement a feature. Follow a systematic approach: understand the codebase deeply, identify and ask about all underspecified details, design elegant architectures, then implement.

## Core Principles

- **Ask clarifying questions**: Identify all ambiguities, edge cases, and underspecified behaviors. Ask specific, concrete questions rather than making assumptions. Wait for user answers before proceeding with implementation. Ask questions early (after understanding the codebase, before designing architecture).
- **Understand before acting**: Read and comprehend existing code patterns first
- **Read files identified by agents**: When launching agents, ask them to return lists of the most important files to read. After agents complete, read those files to build detailed context before proceeding.
- **Simple and elegant**: Prioritize readable, maintainable, architecturally sound code
- **Use TodoWrite**: Track all progress throughout
- **Leverage existing specs**: Check for PLAN.md or SPEC.md files and use them to guide development
- **Use AskUserQuestion tool**:
  - Generate **2-4 questions** per iteration,
  - Each question has **2-4 concrete options**
  - Each option includes brief **pros/cons**
  - Avoid open-ended questions - provide specific choices
  - "Other" option is auto-added - don't include it
  - Continue iterations until ALL unclear points are resolved

---

## Phase 1: Discovery

**Goal**: Understand what needs to be built

**Actions**:

1. Create todo list with all phases
2. **Search for existing PLAN.md or SPEC.md files** in the project using Glob tool:
   - If found, read and analyze their contents
   - Use this specification to inform all subsequent phases
3. Summarize understanding and confirm with user.

---

## Phase 2: Codebase Exploration

**Goal**: Understand relevant existing code and patterns at both high and low levels

**Actions**:

1. Launch 2-3 code-explorer agents in parallel. Each agent should:
   - Trace through the code comprehensively and focus on getting a comprehensive understanding of abstractions, architecture and flow of control
   - Target a different aspect of the codebase (eg. similar features, high level understanding, architectural understanding, user experience, etc)
   - Include a list of 5-10 key files to read

   **Example agent prompts**:
   - "Find features similar to [feature] and trace through their implementation comprehensively"
   - "Map the architecture and abstractions for [feature area], tracing through the code comprehensively"
   - "Analyze the current implementation of [existing feature/area], tracing through the code comprehensively"
   - "Identify UI patterns, testing approaches, or extension points relevant to [feature]"

2. Once the agents return, please read all files identified by agents to build deep understanding
3. Present comprehensive summary of findings and patterns discovered

---

## Phase 3: Clarifying Questions

**Goal**: Fill in gaps and resolve all ambiguities before designing

**CRITICAL**: This is one of the most important phases. DO NOT SKIP.

**Actions**:

1. Review the codebase findings, original feature request, and any PLAN.md/SPEC.md contents
2. **Use the `/clarify:clarify` command** to systematically clarify requirements:
3. Document all clarified requirements
4. **Update PLAN.md or SPEC.md** with the clarified specifications

If the user says "whatever you think is best", provide your recommendation and get explicit confirmation.

---

## Phase 4: Architecture Design

**Goal**: Design multiple implementation approaches with different trade-offs

**Actions**:

1. Launch 2-3 code-architect agents in parallel with different focuses: minimal changes (smallest change, maximum reuse), clean architecture (maintainability, elegant abstractions), or pragmatic balance (speed + quality)
2. Review all approaches and form your opinion on which fits best for this specific task (consider: small fix vs large feature, urgency, complexity, team context)
3. Present to user: brief summary of each approach, trade-offs comparison, **your recommendation with reasoning**, concrete implementation differences
4. **Ask user which approach they prefer**
5. **Update PLAN.md or SPEC.md** with the chosen architecture and rationale

---

## Phase 5: Task Decomposition

**Goal**: Break down the implementation into manageable, trackable tasks

**CRITICAL**: This phase must be completed before starting implementation.

**Actions**:

1. **Use the `/decomposition:decomposition` command** to break down the feature into detailed, actionable tasks
2. Review the generated task breakdown with the user
3. Ensure each task is:
   - Small enough to complete independently
   - Has clear acceptance criteria
   - Properly ordered by dependencies
4. **Update PLAN.md or SPEC.md** with the task breakdown

---

## Phase 6: Implementation

**Goal**: Build the feature

**DO NOT START WITHOUT USER APPROVAL**

**Actions**:

1. Wait for explicit user approval
2. Read all relevant files identified in previous phases
3. Implement following chosen architecture and task breakdown from Phase 4.5
4. Follow codebase conventions strictly
5. Write clean, well-documented code
6. Update todos as you progress
7. **Update PLAN.md or SPEC.md** with implementation progress and any design decisions made during development

---

## Phase 7: Quality Review

**Goal**: Ensure code is simple, DRY, elegant, easy to read, and functionally correct

**Actions**:

1. **Use the `pr-review-toolkit:review-pr` agent** for comprehensive PR review
2. **Use the `code-reviewer` agent**
3. Consolidate findings and identify highest severity issues that you recommend fixing
4. **Present findings to user and ask what they want to do** (fix now, fix later, or proceed as-is)
5. Address issues based on user decision
6. **Update PLAN.md or SPEC.md** with any changes made during review

---

## Phase 8: Summary

**Goal**: Document what was accomplished

**Actions**:

1. Mark all todos complete
2. Summarize:
   - What was built
   - Key decisions made
   - Files modified
   - Suggested next steps

---
