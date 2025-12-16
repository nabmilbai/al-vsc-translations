# Optimized NAB AL Tools Translation Workflow

This repository contains an optimized set of AI agent configuration files for automating Business Central translations using [NAB AL Tools](https://github.com/jwikman/nab-al-tools) by NAB Solutions AB.

## 🚀 Quick Start (The Only File You Need)

**al-translate-xlf.prompt.md** is the master trigger.
*   **Command**: /al-translate-xlf
*   **Action**: Builds the app, syncs XLF files, and translates all untranslated texts automatically.
*   **Logic**: It uses the al-translator.agent.md agent and follows the strict rules in al-translate-xlf.instructions.md.

---

## 📂 Files Overview

### 1. Core Workflow (Required)
These files work together to handle the entire translation process.

*   **al-translate-xlf.prompt.md (Trigger)**:
    *   The entry point. Use this to start translating.
    *   Automatically handles the "Swedish First" policy for Nordic languages.

*   **al-translator.agent.md (Agent)**:
    *   The AI worker definition. It has access to the build, sync, and translation tools.
    *   Orchestrates the loop: Build -> Refresh -> Translate -> Save.

*   **al-translate-xlf.instructions.md (Rules)**:
    *   The "Brain". Contains the strict rules (e.g., "Never translate app names", "Preserve placeholders").
    *   Handles glossary merging logic automatically.

### 2. Optional Utilities (Advanced)
You do **not** need these for standard translation, but they are useful for maintenance.
*   **al-review-translations.prompt.md**:
    *   **Command**: /al-review-translations
    *   **Purpose**: Quality Assurance. Checks existing translations for glossary compliance and placeholder errors. Useful for fixing "needs-review" states.
*   **al-update-glossary.prompt.md**:
    *   **Command**: /al-update-glossary
    *   **Purpose**: Terminology Discovery. Scans your source code to find common terms that *should* be in your glossary but aren't.

## 🛠️ Usage

### Prerequisites
1.  **VS Code Extension**: [NAB AL Tools](https://marketplace.visualstudio.com/items?itemName=nabsolutions.nab-al-tools) installed.
2.  **Project**: An open Business Central app (folder with app.json).

### How to Translate
1.  Open the **Copilot Chat** in VS Code.
2.  Type **/al-translate-xlf** and press Enter.
3.  Sit back. The agent will:
    *   Build the app.
    *   Sync the XLF files.
    *   Translate in batches of 100.
    *   Save progress automatically.

## 🧠 Glossary Handling
*   **Standard**: The agent automatically uses standard Business Central terminology.
*   **Custom**: If you have a glossary.tsv in your Translations folder, the agent automatically merges it with the standard terms. You don't need to do anything extra.

## 🔄 Handling [NAB: REVIEW] Tags

When source texts change in the .g.xlf file, existing translations may no longer be accurate. NAB AL Tools automatically flags these with [NAB: REVIEW] in the target text.

### What It Means
- The source text has been modified since the last translation.
- The current translation might need updating to match the new source.

### How to Handle
1. **Review the Tagged Translation**: Check if the translation still aligns with the new source text.
2. **Update if Necessary**: Modify the translation to reflect changes, preserving placeholders and glossary terms.
3. **Remove the Tag**: Once reviewed and updated, remove [NAB: REVIEW] from the target text.
4. **Save and Sync**: Use NAB AL Tools to save changes and refresh the XLF file.

This ensures translation quality and prevents outdated or incorrect translations from persisting.

---

*Disclaimer: These files are derived from and optimized for the NAB AL Tools extension by NAB Solutions AB.*
