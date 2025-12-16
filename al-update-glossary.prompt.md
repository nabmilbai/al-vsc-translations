---
agent: al-translator
description: 'Update Glossary'
tools: ['nabsolutions.nab-al-tools/getGlossaryTerms', 'nabsolutions.nab-al-tools/getTextsToTranslate']
---

Analyze the source texts in the XLF files to identify common business terms that are missing from the glossary.

1. **Fetch Glossary**: Call `getGlossaryTerms` to see current entries.
2. **Scan Texts**: Call `getTextsToTranslate` to get a sample of source texts.
3. **Identify Candidates**: Find frequently used terms (e.g., "Invoice", "Customer", "Posting") that are NOT in the glossary.
4. **Output**: Generate a TSV-formatted block of suggested additions for `glossary.tsv`.

Format:
English	TargetLanguage	Description
Term	Translation	Context
