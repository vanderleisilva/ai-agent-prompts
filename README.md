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

## AI Code Confidence Pipeline — Task × Model Matrix

| Task | Purpose | What the agent does | Suggested model |
|-----|--------|---------------------|-----------------|
| **Brainstorming / Ideation** | Explore solution space and trade-offs | Proposes multiple approaches, highlights pros/cons, surfaces key assumptions and architectural trade-offs. No code. | **Strong reasoning model** (GPT-4.1 / GPT-4o / Claude Sonnet) |
| **Code generation** | Produce clear, minimal implementation | Writes the simplest correct implementation following conventions. No explanations, no tests, no self-approval. | **Fast / cheap model** (GPT-4o-mini, Claude Haiku, Cursor Fast) |
| **Senior code review** | Surface risks and design smells | Critically reviews code for hidden assumptions, edge cases, maintainability, and production risks. | **Strongest reasoning model** (GPT-4.1 / Claude Sonnet / Cursor Best) |
| **Adversarial / breaker** | Stress-test behavior | Actively tries to break the code by imagining realistic failure scenarios, misuse, scale, and concurrency issues. | **Strong reasoning model** (same as reviewer or one tier below) |
| **Test generation** | Prove correctness and prevent regressions | Writes minimal, high-signal tests that fail if behavior is incorrect or regresses. | **Strong (not max)** (GPT-4o / Claude Sonnet) |
| **Confidence summary** | Decide trust and merge readiness | Synthesizes all findings and assigns a confidence level (Low / Medium / High) with explicit assumptions and risks. | **Strongest reasoning model** (same as reviewer) |

> **Principle:** Creation and judgment are always separated.  
> Models are optimized for their role: fast models type code, strong models reason about risk.

## Usage

These prompts can be used in various, bellow follows some ideas depending on your workflow and tooling:

### Cursor Commands

Create custom commands by storing these prompts in `.cursor/commands/` as Markdown files. Commands are triggered with `/` prefix in the chat input. See the [Cursor Commands documentation](https://cursor.com/docs/context/commands) for details.

**Setup:**

1. Create a `.cursor/commands` directory in your project root
2. Copy the prompt files and rename them as commands (e.g., `generate-code.md`, `review-code.md`)
3. Commands will automatically appear when you type `/` in chat


**Team Commands:**

For Team and Enterprise plans, create commands in the [Cursor Dashboard](https://cursor.com/dashboard?tab=team-content&section=commands) to share standardized workflows across your organization.

### Cursor Rules

Store these prompts as Project Rules in `.cursor/rules/` to guide AI behavior. Rules are version-controlled and can be scoped to specific files or applied intelligently. See the [Cursor Rules documentation](https://cursor.com/docs/context/rules) for details.


**Team Rules:**

For Team and Enterprise plans, create rules in the [Cursor Dashboard](https://cursor.com/dashboard?tab=team-content) to enforce standards across your organization. Team Rules take precedence over Project Rules.

**Integration with commands:**

Rules work alongside commands - rules set the default behavior, while commands provide specific workflows. For example, your rules might enforce code generation principles, while `/review-code` command provides a detailed review workflow.

### CI/CD Integration

Automate quality checks in your pipeline:

- **Pre-commit hooks**: Run code review and adversarial analysis before commits
- **Pull Request checks**: Use the multi-agent workflow to review PRs automatically
- **Continuous monitoring**: Integrate confidence scoring into your deployment pipeline
- **Test generation**: Automatically generate tests for new code changes

### Manual Workflow

Use these prompts interactively:

1. (Optional) Start with `brainstorming.md` to explore multiple approaches and trade-offs before implementation
2. Use `code-generation.md` to write initial implementation
3. Apply `code-review.md` for critical review
4. Run `adversarial-breaker.md` to identify edge cases
5. Use `test-generation.md` to create comprehensive tests
6. Finish with `confidence-summary.md` for final assessment


## Contents

- **prompt-workflow.md** - Guide for selecting the right AI model and prompt approach for different development tasks
- **brainstorming.md** - Prompt for exploring multiple solution approaches, trade-offs, and architectural considerations
- **code-generation.md** - Prompt for writing simple, straightforward production code
- **code-review.md** - Automated code confidence pipeline prompt
- **adversarial-breaker.md** - Prompt for identifying realistic failure scenarios in production code
- **test-generation.md** - Prompt for writing minimal tests that catch failures and regressions
- **confidence-summary.md** - Prompt for assigning confidence levels and risk assessment

