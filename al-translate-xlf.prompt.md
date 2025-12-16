---
agent: al-translator
description: 'Translate XLF Files'
tools: ['search/codebase', 'search', 'nabsolutions.nab-al-tools/getTextsToTranslate', 'nabsolutions.nab-al-tools/getTranslatedTextsByState', 'nabsolutions.nab-al-tools/getTranslatedTextsMap', 'nabsolutions.nab-al-tools/refreshXlf', 'nabsolutions.nab-al-tools/saveTranslatedTexts', 'nabsolutions.nab-al-tools/getGlossaryTerms', 'ms-dynamics-smb.al/al_build']
---

Translate the current app according to the l-translate-xlf.instructions.md and l-translator.agent.md.

1. **Identify App**: Locate the pp.json and Translations folder.
2. **Build**: Run l_build to ensure g.xlf is current.
3. **Process Files**: For each XLF file in the Translations folder:
   - Sync using efreshXlf.
   - Fetch glossary using getGlossaryTerms (this handles local glossary.tsv automatically).
   - Translate iteratively using getTextsToTranslate and saveTranslatedTexts.
   - Follow the Nordic Policy (Swedish first) if applicable.
4. **Review**: Ensure all texts are translated and glossary terms are applied.
5. **Summary**: Provide a summary table of challenging translations as per the agent instructions.

Proceed automatically and continuously.
