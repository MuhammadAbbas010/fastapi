### Target language

Translate to Urdu (اردو).

Language code: ur.

### Script and Alignment

* Use Arabic script (Nastaliq) for Urdu text.
* Wrap translated body in `<div dir="rtl" style="text-align: right;">...</div>` so headings, paragraphs, and lists render right-aligned. 
* Where an English/Latin-script term sits directly next to Urdu text, add one extra space around it, so the two scripts don't visually run together.

### Punctuation

* Always use the Urdu full stop `۔` instead of the English period `.` at the end of sentences.
* Bold colons in translated prose (`:` → `**:**`) for readability.
* Do not bold colons inside code blocks, inline code, paths, URLs, or anything wrapped in backticks.

### Ellipsis
* Keep a space between an ellipsis (`...`) and the word before or after it.

Examples:

Source (English):
```
...as we intended.
...this would work:
...etc.
others...
More to come...
```

Result (Urdu):
```
... جیسا کہ ہمارا ارادہ تھا۔
... یہ اس طرح کام کرے گا**:**
... وغیرہ۔
دیگر ...
مزید جلد ...
```

* This spacing rule does not apply inside URLs, code blocks, or code snippets — never add or remove spaces there.

### Technical Terms

* Do not translate everything. Keep common programming terms in English as-is (e.g. framework, endpoint, plug-in, payload).
* Exception: words commonly understood in transliterated form even by Urdu speakers (e.g. "install" → "انسٹال") may be transliterated.
* Keep class names, function names, modules, file names, and CLI commands unchanged — never translate or transliterate these.
* Keep infinitive verbs as infinitives where appropriate (e.g. "to install" → "انسٹال کرنا"). Do not unnecessarily conjugate or restructure verbs.
* Keep all code, commands, filenames, and technical terms unchanged.

### What Not to Translate

* Proper nouns / product names: FastAPI, Pydantic, SQLModel, PostgreSQL, React, TypeScript, Docker Compose, Traefik, Pytest, Playwright, GitHub Actions, etc.
* Anything inside backticks, code blocks, file paths, and URLs.
* * Do not convert or restyle quotes inside code blocks, inline code, paths, URLs, or anything wrapped in backticks. Only adjust quote style in translated prose.
* Anchor tags in headings (`{ #anchor-id }`).
