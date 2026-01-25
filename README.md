# AI Agents Prompts

A collection of prompts and workflows for AI-assisted software development, focusing on code review, adversarial testing, and quality assurance.

## Description

This project uses a **multi-agent AI workflow** to assist with code generation while maintaining high confidence in correctness and maintainability.

Instead of relying on a single AI agent (or “auto” mode) to write and approve code, responsibilities are explicitly separated across multiple roles:

- **Code Generator** – writes the simplest possible implementation, focused on clarity and conventions.

- **Senior Reviewer** – critically reviews the code for hidden assumptions, design smells, and production risks.

- **Adversarial / Breaker** – actively tries to break the code by imagining realistic failure scenarios.

- **Test Generator** – writes tests that would fail if the implementation is incorrect or regresses.

- **Confidence Summary** – synthesizes all findings and assigns a confidence level (Low / Medium / High).

Each step acts as a confidence gate. Code is trusted not because the AI says it is correct, but because it has been reviewed, challenged, and proven through tests.

## Contents

- **prompt-workflow.md** - Guide for selecting the right AI model and prompt approach for different development tasks
- **code-generation.md** - Prompt for writing simple, straightforward production code
- **code-review.md** - Automated code confidence pipeline prompt
- **adversarial-breaker.md** - Prompt for identifying realistic failure scenarios in production code
- **test-generation.md** - Prompt for writing minimal tests that catch failures and regressions
- **confidence-summary.md** - Prompt for assigning confidence levels and risk assessment

