---
agent: al-translator
description: 'Review Translations'
tools: ['nabsolutions.nab-al-tools/getTranslatedTextsByState', 'nabsolutions.nab-al-tools/saveTranslatedTexts', 'nabsolutions.nab-al-tools/getGlossaryTerms']
---

Review the existing translations for quality and consistency.

1. **Fetch Translations**: Call `getTranslatedTextsByState` (filter for 'needs-review' first, then 'translated').
2. **Fetch Glossary**: Call `getGlossaryTerms` to verify compliance.
3. **Review Criteria**:
   - Glossary terms must be used.
   - Placeholders (%1) must be preserved.
   - No app name translation.
4. **Action**:
   - If a translation is incorrect, fix it using `saveTranslatedTexts`.
   - If correct but marked 'needs-review', save it as 'translated'.
5. **Report**: Summarize any corrections made.
