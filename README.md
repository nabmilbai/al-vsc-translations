# Optimized NAB AL Tools Translation Workflow

This repository contains an optimized set of AI agent configuration files for automating Business Central translations using [NAB AL Tools](https://github.com/jwikman/nab-al-tools) by NAB Solutions AB.

These files are refined versions of the original NAB AL Tools prompts and agents, optimized for better consistency, "DRY" (Don't Repeat Yourself) principles, and improved glossary handling.

## Files Overview

### Core Workflow
*   **l-translate-xlf.instructions.md (The Brain)**:
    *   Contains the core rules, invariants, and step-by-step logic for the translation workflow.
    *   Enforces the "Swedish First" policy for Nordic languages.
    *   Handles glossary logic via getGlossaryTerms (merging local and built-in glossaries automatically).

*   **l-translator.agent.md (The Body)**:
    *   Defines the AI Agent, its available tools, and the high-level execution loop.
    *   Orchestrates the build -> sync -> translate -> review cycle.

*   **l-translate-xlf.prompt.md (The Trigger)**:
    *   The main entry point to start the translation task.
    *   References the Agent and Instructions to avoid logic duplication.

### Auxiliary Prompts
*   **l-update-glossary.prompt.md**:
    *   Scans the app's source texts to identify common terms missing from the glossary.
    *   Suggests new entries for glossary.tsv.

*   **l-review-translations.prompt.md**:
    *   Performs a quality check on existing translations.
    *   Verifies glossary usage and placeholder integrity.
    *   Fixes or approves translations marked as "needs-review".

## Usage

### 1. Prerequisites
*   VS Code with [NAB AL Tools](https://marketplace.visualstudio.com/items?itemName=nabsolutions.nab-al-tools) extension installed.
*   An active Business Central project with an pp.json and Translations folder.
*   (Optional) A glossary.tsv file in the Translations folder for project-specific terms.

### 2. Invoking Prompts
You do **not** need to copy and paste the prompt content. If these files are placed in your configured prompts folder (e.g., .github/prompts or your user prompts folder), you can invoke them directly in GitHub Copilot Chat using the / command followed by the filename (or name defined in the file).

**Examples:**
*   **Start Translation**: Type /al-translate-xlf
*   **Update Glossary**: Type /al-update-glossary
*   **Review Translations**: Type /al-review-translations

Copilot will automatically load the instructions and execute the defined workflow.

## Optimizations Applied

*   **Automated Glossary Merging**: Removed manual file parsing; relies on getGlossaryTerms to merge local glossary.tsv with standard terms.
*   **Unified Tool Naming**: Standardized tool calls to match the extension's namespace.
*   **Mandatory Build Step**: Enforces l_build before translation to ensure g.xlf is current.
*   **Simplified Prompting**: Decoupled the trigger prompt from the workflow logic to prevent drift.

---
*Disclaimer: These files are derived from and optimized for the NAB AL Tools extension by NAB Solutions AB. They are intended to enhance the AI-assisted translation experience within that ecosystem.*
