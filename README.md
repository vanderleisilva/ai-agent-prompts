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

1. Start with `code-generation.md` to write initial implementation
2. Apply `code-review.md` for critical review
3. Run `adversarial-breaker.md` to identify edge cases
4. Use `test-generation.md` to create comprehensive tests
5. Finish with `confidence-summary.md` for final assessment


## Contents

- **prompt-workflow.md** - Guide for selecting the right AI model and prompt approach for different development tasks
- **code-generation.md** - Prompt for writing simple, straightforward production code
- **code-review.md** - Automated code confidence pipeline prompt
- **adversarial-breaker.md** - Prompt for identifying realistic failure scenarios in production code
- **test-generation.md** - Prompt for writing minimal tests that catch failures and regressions
- **confidence-summary.md** - Prompt for assigning confidence levels and risk assessment

