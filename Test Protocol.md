# How to Test the NAB AL Translator Agent

This guide explains how to verify that the AI translation workflow is working correctly in your Business Central project.

## Prerequisites
1.  **VS Code** is open.
2.  **NAB AL Tools** extension is installed and enabled.
3.  You have the **PrintVis-Toolbox** repository open (or any valid AL project).
4.  You are in the `App` folder (where `app.json` resides).

---

## Test Scenario 1: The Main Translation Workflow (Core)

**Goal**: Verify that the agent can build, sync, and translate untranslated texts.

### Steps:
1.  **Open a File**: Open any file within the `App` folder (e.g., `App/app.json`) to ensure the agent knows which app to work on.
2.  **Open Copilot Chat**: Click the Chat icon in the sidebar.
3.  **Run the Command**: Type the following and press Enter:
    ```
    /al-translate-xlf
    ```
4.  **Observe the Agent**:
    *   It should first run `al_build` (you might see a build notification or terminal output).
    *   It should run `refreshXlf` to sync the translation files.
    *   It should announce it is fetching texts (e.g., "Fetching 100 texts...").
    *   It should start saving translations in batches.
5.  **Verify Results**:
    *   Go to the `App/Translations` folder.
    *   Open one of the `.xlf` files (e.g., `NAB PrintVis Toolbox.sv-SE.xlf`).
    *   Check if previously empty `<target>` tags are now filled.
    *   Check `git diff` to see the changes.

---

## Test Scenario 2: Glossary Integration (Optional)

**Goal**: Verify that the agent uses the glossary correctly.

### Steps:
1.  **Check Glossary**: Ensure `App/Translations/glossary.tsv` exists. If not, create a dummy one:
    ```tsv
    English	Swedish
    TestTerm	TestTermSvenska
    ```
2.  **Create a Test Text**: Add a label in an AL file with the content "TestTerm".
3.  **Run Translation**: Run `/al-translate-xlf` again.
4.  **Verify**: Check if "TestTerm" was translated to "TestTermSvenska" in the XLF file.

---

## Test Scenario 3: Review Translations (Optional)

**Goal**: Verify the quality assurance prompt.

### Steps:
1.  **Run the Command**:
    ```
    /al-review-translations
    ```
2.  **Observe**: The agent should scan existing translations and report if any "needs-review" items were found or if glossary terms were missed.

---

## Troubleshooting

*   **"No app found"**: Make sure you have a file open from the `App` folder.
*   **"Agent not found"**: Ensure the prompt files are in the correct `.vscode/prompts` or user prompts directory.
*   **"Build failed"**: Fix any AL compilation errors before translating.
