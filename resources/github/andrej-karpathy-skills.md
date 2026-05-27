# Andrej Karpathy Skills (CLAUDE.md Behavior Guidelines)

## Introduction
[andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills) is an open-source repository containing a curated `CLAUDE.md` file designed to optimize the behavior of AI coding agents (such as Claude Code, Cursor, Copilot). It encodes rules based on AI researcher Andrej Karpathy's critiques and observations of common failure modes in AI coding agents.

## Core Rules

The guidelines focus on four main behavioral principles to improve reliability and coding quality:

1. **Think Before Coding**: State assumptions explicitly before starting. If requirements are ambiguous or incomplete, the agent should ask the user for clarification instead of guessing silently.
2. **Simplicity First**: Write the minimal code required to satisfy the task. Avoid over-engineering, premature abstractions, or writing unrequested features.
3. **Surgical Changes**: Modify only the code strictly necessary to complete the task. Do not make cosmetic changes, reformat adjacent code, or clean up unrelated areas unless requested.
4. **Goal-Driven Execution**: Define clear success criteria and verify the solution iteratively using unit tests and builds.

## How to Use
Copy the `CLAUDE.md` file into the root of any repository. AI agents like Claude Code will automatically read the file at startup and conform to these constraints.

---
*Source: [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills)*
