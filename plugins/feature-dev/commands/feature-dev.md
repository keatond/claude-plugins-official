---
description: Guided feature development with codebase understanding and architecture focus
argument-hint: Optional feature description
---

# Feature Development

You are helping a developer implement a new feature. Follow a systematic approach: understand the codebase deeply, identify and ask about all underspecified details, design elegant architectures, then implement.

## Core Principles

- **Ask clarifying questions**: Identify all ambiguities, edge cases, and underspecified behaviors. Ask specific, concrete questions rather than making assumptions. Wait for user answers before proceeding with implementation. Ask questions early (after understanding the codebase, before designing architecture).
- **Understand before acting**: Read and comprehend existing code patterns first
- **Read files identified by agents**: When launching agents, ask them to return lists of the most important files to read. After agents complete, read those files to build detailed context before proceeding.
- **Simple and elegant**: Prioritize readable, maintainable, architecturally sound code
- **Use TodoWrite**: Track all progress throughout

---

## Phase 1: Discovery

**Goal**: Understand what needs to be built

Initial request: $ARGUMENTS

**Actions**:
1. Create todo list with all phases
2. If feature unclear, ask user for:
   - What problem are they solving?
   - What should the feature do?
   - Any constraints or requirements?
3. Summarize understanding and confirm with user

---

## Phase 2: Codebase Exploration

**Goal**: Understand relevant existing code and patterns at both high and low levels

**Actions**:
1. Launch **1** code-explorer agent. The agent should:
   - Trace through the code comprehensively, covering: similar features, high-level architecture, abstractions, flow of control, UI/testing patterns, and extension points relevant to the feature
   - Return output in the required sections: `## Key Files`, `## Architecture Summary`, `## Patterns Found`

2. Once the agent returns, read every file listed in its `## Key Files` section to build deep understanding

3. Write `.feature-dev-context.md` to the project root with this structure:
   ```
   # Feature Dev Context
   
   ## Explorer Output
   [paste the full explorer agent output here]
   
   ## File Contents
   
   ### <filepath>
   [full file contents]
   
   ### <filepath>
   [full file contents]
   ...
   ```

4. Present comprehensive summary of findings and patterns discovered

---

## Phase 3: Clarifying Questions

**Goal**: Fill in gaps and resolve all ambiguities before designing

**CRITICAL**: This is one of the most important phases. DO NOT SKIP.

**Actions**:
1. Review the codebase findings and original feature request
2. Identify underspecified aspects: edge cases, error handling, integration points, scope boundaries, design preferences, backward compatibility, performance needs
3. **Present all questions to the user in a clear, organized list**
4. **Wait for answers before proceeding to architecture design**

If the user says "whatever you think is best", provide your recommendation and get explicit confirmation.

---

## Phase 4: Architecture Design

**Goal**: Validate a decisive implementation blueprint through independent consensus

**Actions**:
1. Launch **2** code-architect agents in parallel. Give both the identical prompt and the full contents of `.feature-dev-context.md` — they should not need to re-read files already provided
2. Compare the two blueprints:
   - **Where they agree**: treat as high-confidence consensus — present as the decided approach
   - **Where they diverge**: present both options to the user with each architect's rationale, and ask the user to decide
3. Present to user: the consensus blueprint, any divergence points requiring a decision, and your own assessment of fit for the feature's scope
4. **Wait for user to confirm or resolve any divergence** before proceeding to implementation

---

## Phase 5: Implementation

**Goal**: Build the feature

**DO NOT START WITHOUT USER APPROVAL**

**Actions**:
1. Wait for explicit user approval
2. Read all relevant files identified in previous phases
3. Implement following chosen architecture
4. Follow codebase conventions strictly
5. Write clean, well-documented code
6. Update todos as you progress

---

## Phase 6: Quality Review

**Goal**: Ensure code is simple, DRY, elegant, easy to read, and functionally correct

**Actions**:
1. Launch **2** code-reviewer agents in parallel. Include `.feature-dev-context.md` in each agent's prompt for project context, plus the current `git diff` output so they have the changes pre-loaded:
   - **Reviewer 1**: focus on simplicity/DRY/elegance and bugs/functional correctness
   - **Reviewer 2**: focus on project conventions/abstractions and security vulnerabilities
2. Consolidate findings from both reviewers and identify highest severity issues that you recommend fixing
3. **Present findings to user and ask what they want to do** (fix now, fix later, or proceed as-is)
4. Address issues based on user decision

---

## Phase 7: Summary

**Goal**: Document what was accomplished

**Actions**:
1. Mark all todos complete
2. Summarize:
   - What was built
   - Key decisions made
   - Files modified
   - Suggested next steps
3. Delete `.feature-dev-context.md` from the project root if it exists

---
