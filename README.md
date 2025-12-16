# Optimized NAB AL Tools Translation Workflow

This repository contains an optimized set of AI agent configuration files for automating Business Central translations using [NAB AL Tools](https://github.com/jwikman/nab-al-tools) by NAB Solutions AB.

These files are refined versions of the original NAB AL Tools prompts and agents, optimized for better consistency, "DRY" (Don't Repeat Yourself) principles, and improved glossary handling.

## Files Overview

*   **`translate-xlf.instructions.md` (The Brain)**:
    *   Contains the core rules, invariants, and step-by-step logic for the translation workflow.
    *   Enforces the "Swedish First" policy for Nordic languages.
    *   Handles glossary logic via `getGlossaryTerms` (merging local and built-in glossaries automatically).

*   **`al-translator.agent.md` (The Body)**:
    *   Defines the AI Agent, its available tools, and the high-level execution loop.
    *   Orchestrates the build -> sync -> translate -> review cycle.

*   **`translate-xlf.prompt.md` (The Trigger)**:
    *   A simplified entry point to start the translation task.
    *   References the Agent and Instructions to avoid logic duplication.

## Usage

1.  **Prerequisites**:
    *   VS Code with [NAB AL Tools](https://marketplace.visualstudio.com/items?itemName=nabsolutions.nab-al-tools) extension installed.
    *   An active Business Central project with an `app.json` and `Translations` folder.
    *   (Optional) A `glossary.tsv` file in the `Translations` folder for project-specific terms.

2.  **Execution**:
    *   Open `translate-xlf.prompt.md`.
    *   Copy the content.
    *   Paste it into GitHub Copilot Chat (or your AI assistant) to trigger the workflow.

## Optimizations Applied

*   **Automated Glossary Merging**: Removed manual file parsing; relies on `getGlossaryTerms` to merge local `glossary.tsv` with standard terms.
*   **Unified Tool Naming**: Standardized tool calls to match the extension's namespace.
*   **Mandatory Build Step**: Enforces `al_build` before translation to ensure `g.xlf` is current.
*   **Simplified Prompting**: Decoupled the trigger prompt from the workflow logic to prevent drift.

---
*Disclaimer: These files are derived from and optimized for the NAB AL Tools extension by NAB Solutions AB. They are intended to enhance the AI-assisted translation experience within that ecosystem.*
