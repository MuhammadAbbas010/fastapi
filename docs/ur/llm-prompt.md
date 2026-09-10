### Target language

Translate to Urdu (اردو).

Language code: ur.

Keep existing translations as they are if the term is already translated. Only change an existing translation if it contradicts a rule below.

Only keep parentheses if they exist in the source text. Do not add parentheses to terms that do not have them.

### Script and Alignment

* Use Arabic script (Nastaliq) for Urdu text.
* Wrap the translated body in `<div dir="rtl" style="direction: rtl; text-align: right;">...</div>` so headings, paragraphs, and lists render right-aligned. Leave a blank line after the opening tag and before the closing tag.
* Always set direction **twice**: once as the `dir` attribute and once as `direction` inside the inline `style`. They are not redundant. Some renderers and HTML sanitizers drop the `dir` attribute while keeping inline styles, and when that happens `dir` alone silently does nothing — headings and paragraphs still right-align from `text-align`, but list bullets stay on the left because bullet placement is governed by `direction`, not by alignment.
* Everything inside the wrapper inherits from it, so **do not** add `dir` or `style` to individual headings, paragraphs, lists, or list items. Markdown-generated `<ul>` and `<h2>` elements cannot carry attributes anyway without rewriting them as raw HTML, which would make the translation impossible to diff against the English source.
* Bulleted and numbered lists are always right-to-left, with the bullet on the right, whatever script the item starts with. A list item beginning with `you`, `GTD`, or `` `foo` `` is still an RTL line.
* Where an English/Latin-script term sits directly next to Urdu text, add one extra space around it, so the two scripts don't visually run together.
* When a **heading** begins with a Latin-script word, prefix the heading text with `&rlm;` (U+200F). Without it the bidi algorithm takes the line's base direction from that first Latin character and lays the whole heading out left-to-right. The `&rlm;` renders as nothing and keeps the heading aligned right.

Example:

```
### &rlm;abbr مکمل فقرہ دیتا ہے { #the-abbr-gives-a-full-phrase }
### &rlm;Superclasses اور subclasses { #super-and-subclasses }
```

* Place the `&rlm;` after the `#` characters and the space, at the very start of the heading text. Never place it inside the `{ #anchor-id }` part.

### Code blocks are always left-aligned

Code is read left-to-right in every language. A code block must never shift to the right side of the page, and this holds whether the block's first line is English, is a translated Urdu comment, or is blank.

* Wrap every fenced code block in `<div dir="ltr" style="direction: ltr; text-align: left;">`, with a blank line after the opening tag and before the closing tag. This follows the same pattern the English docs already use for `<div class="termy">`.
* As with the outer wrapper, the direction must be set both as the `dir` attribute and as `direction` in the inline style. With only the attribute, a block whose first line is a translated Urdu comment inherits RTL from the page wrapper and flips to the right, while a block whose first line is English stays left — giving inconsistent alignment across the same page.

Example:

```
<div dir="ltr" style="direction: ltr; text-align: left;">

​```Python
wont_work()  # یہ کام نہیں کرے گا
​```

</div>
```

* Where the English source already wraps the block in `<div class="termy">`, add the attributes to that existing element rather than nesting a second one: `<div class="termy" dir="ltr" style="direction: ltr; text-align: left;">`.
* Never add `dir` to the fence itself, and never change the indentation or line order inside a block to influence its direction.
* A cleaner alternative, if the build allows a language-specific stylesheet, is a single CSS rule instead of the wrappers. See the appendix at the end of this file.

### Punctuation

* Always use the Urdu full stop `۔` instead of the English period `.` at the end of sentences.
* Bold colons in translated prose (`:` → `**:**`) for readability.
* Do not bold colons inside code blocks, inline code, paths, URLs, or anything wrapped in backticks.

### Quotes

* Keep the default English neutral quotes (`"` and `'`). Do not convert them to typographic or angled quotation marks.
* Place the sentence-final full stop **inside** the closing quotation mark, as Urdu punctuation requires — not outside it as English does.

Examples:

Source (English):
```
My friend wrote: "This is how it works".
He answered: "Correct, but 'this' is not '"this"'".
```

Result (Urdu):
```
میرے دوست نے لکھا**:** "یہ اس طرح کام کرتا ہے۔"
اس نے جواب دیا**:** "درست، لیکن 'this' ، '"this"' نہیں ہے۔"
```

* Do not convert or restyle quotes inside code blocks, inline code, paths, URLs, or anything wrapped in backticks. Only adjust quote style in translated prose.

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

### Headings

* Leave the hash part inside curly brackets (`{ #anchor-id }`) completely unchanged. This is a hard rule — changing it breaks every link pointing at that heading.
* Translate the ordinary words of the heading into Urdu.
* Where the Urdu translation is a casual, everyday word, use the translation: `Headings` → `سرخیاں`, `Quotes` → `واوین`, `Code snippets` → `کوڈ کے ٹکڑے`.
* **Never transliterate an English technical term, acronym, or initialism into Urdu script.** `HTML` stays `HTML`, not `ایچ ٹی ایم ایل`. `LLM` stays `LLM`, not `ایل ایل ایم`. The same applies to `API`, `SDK`, `CLI`, `JSON`, `HTTP`, `CPU`, `RAM`, and to multi-word technical terms such as `Type hints` and `Deep Learning`.
* Keep proper nouns and product names in English: `FastAPI`, `Pydantic`, `OpenAPI`, `Starlette`, `Python`, `GitHub`.
* Keep literal identifiers as identifiers: an HTML tag name like `abbr`, a class name like `APIRouter`, a filename like `main.py`.
* Everyday loanwords that Urdu speakers already say in Urdu are still transliterated, in headings as everywhere else: `link` → `لنک`, `code` → `کوڈ`, `tabs` → `ٹیبز`, `file` → `فائل`.
* A heading may therefore mix scripts. That is correct and expected — `## HTML کے "abbr" عناصر` is right, `## ایچ ٹی ایم ایل کے "abbr" عناصر` is wrong.
* Every heading aligns to the right, including one that begins with an English word. Where it does begin with English, prefix the heading text with `&rlm;` as described under Script and Alignment.

### Code comments

* Translate comments inside code blocks and code snippets into Urdu. Comments are prose, not code.
* This applies to every language: `#` in Python, Bash, and YAML; `//` in JavaScript and in `console` blocks; `<!-- -->` in HTML.
* Never translate the executable code around the comment. Identifiers, string literals, function calls, flags, and paths all stay exactly as they are — including a string that happens to read like English, such as `echo "Hello universe"`.

Example:

Source (English):
```Python
wont_work()  # This won't work 😱
works(foo="bar")  # This works 🎉
```

Result (Urdu):
```Python
wont_work()  # یہ کام نہیں کرے گا 😱
works(foo="bar")  # یہ کام کرتا ہے 🎉
```

### HTML abbr elements

* Never change the visible text of an `<abbr>` element. `I/O` stays `I/O`, `MDN` stays `MDN`.
* In the `title` attribute, keep the English expansion, then a hyphen, then the Urdu translation of that expansion. The reader needs both: the English so the letters of the abbreviation still map to something, the Urdu so the tooltip actually explains it.

Format: `<English expansion> - <Urdu translation>`

Example:

```
<abbr title="Input/Output - ان پٹ / آؤٹ پٹ">I/O</abbr>
```

* Where the English title carries an explanation after a colon, keep the English expansion, add the Urdu translation of the expansion, then translate the explanation into Urdu.

```
<abbr title="Mozilla Developer Network - موزیلا ڈویلپر نیٹ ورک: ڈویلپرز کے لیے دستاویزات ، جو Firefox والوں نے لکھی ہیں">MDN</abbr>
```

* For `<dfn>` elements, translate the whole title into Urdu. Keep the visible term as it is.
* A translation may add its own `<abbr>` elements to explain English words left untranslated. Never remove an `<abbr>` that a previous translation added.

### Technical Terms

* Do not translate everything. Keep common programming terms in English as-is (e.g. framework, endpoint, plug-in, payload).
* Exception: words commonly understood in transliterated form even by Urdu speakers (e.g. "install" → "انسٹال", "link" → "لنک") may be transliterated.
* Keep class names, function names, modules, file names, and CLI commands unchanged — never translate or transliterate these.
* Keep infinitive verbs as infinitives where appropriate (e.g. "to install" → "انسٹال کرنا"). Do not unnecessarily conjugate or restructure verbs.
* Keep all code, commands, filenames, and technical terms unchanged.

### What Not to Translate

* Proper nouns / product names: FastAPI, Pydantic, SQLModel, PostgreSQL, React, TypeScript, Docker Compose, Traefik, Pytest, Playwright, GitHub Actions, etc.
* Anything inside backticks, code blocks, file paths, and URLs.
* Anchor tags in headings (`{ #anchor-id }`).

### Links

* Translate the link text. Leave the link address unchanged.
* The one exception is an absolute link to a page of the FastAPI documentation: point it at the Urdu translation by inserting the language code after the domain.

```
https://fastapi.tiangolo.com/tutorial/  →  https://fastapi.tiangolo.com/ur/tutorial/
```

* This applies to documentation pages only. Absolute links to assets under `/css/`, `/js/`, and `/img/` keep their address unchanged.
* Relative links (`index.md#installation`, `../advanced/index.md`) are never rewritten.

### Special blocks and tab blocks

Add the Urdu translation of the title after a vertical bar (`|`). Where the English block has no title, add one.

- /// note: /// note | نوٹ
- /// note | Technical Details: /// note | تکنیکی تفصیلات
- /// info | Very Technical Details: /// note | نہایت تکنیکی تفصیلات
- /// tip: /// tip | مشورہ
- /// warning: /// warning | انتباہ
- /// danger: /// danger | خطرہ
- /// info: /// info | معلومات
- /// check: /// check | تصدیق
- /// details: /// details | تفصیلات
- //// tab | Test: //// tab | ٹیسٹ
- //// tab | Info: //// tab | معلومات

### Mixed-script list items

A bulleted line that mixes an English term with Urdu splits badly: the bullet and the English sit at one edge of the column and the Urdu at the other, with a gap between them.

* Where a list item pairs an English term with its Urdu rendering, write the **English first**, then a spaced em dash, then the Urdu: `* performance — کارکردگی`.
* Where the term is kept in English with no Urdu rendering, write the English alone: `* request`.
* Where the item is entirely Urdu, write it plainly with no marker.
* Do not prefix list items with `&rlm;`. That marker is for headings only — on a list whose bullet is laid out left-to-right it moves the text away from the bullet and widens the gap instead of closing it.

### List of English terms and their preferred Urdu translations

Below is a list of English terms and their preferred Urdu translations, separated by a colon (:). Use these translations, do not use your own. If an existing translation does not use these terms, update it to use them.

- you: آپ
- your: آپ کا
- e.g.: مثلاً
- etc.: وغیرہ
- the link: لنک
- the docs: دستاویزات
- the documentation: دستاویزات
- the API docs: API دستاویزات
- the automatic docs: خودکار دستاویزات
- the SQLModel docs: SQLModel کی دستاویزات
- the Tutorial - User Guide: ٹیوٹوریل - یوزر گائیڈ
- the Advanced User Guide: ایڈوانسڈ یوزر گائیڈ
- Data Science: Data Science
- Deep Learning: Deep Learning
- Machine Learning: Machine Learning
- Dependency Injection: Dependency Injection
- HTTP Basic authentication: HTTP Basic authentication
- HTTP Digest: HTTP Digest
- ISO format: ISO format
- the JSON Schema standard: JSON Schema معیار
- the JSON schema: JSON schema
- the schema definition: schema کی تعریف
- Password Flow: Password Flow
- Mobile: موبائل
- deprecated: متروک
- designed: ڈیزائن کیا گیا
- invalid: غلط
- valid: درست
- on the fly: موقع پر ہی
- standard: معیاری
- default: ڈیفالٹ
- case-sensitive: case-sensitive
- case-insensitive: case-insensitive
- to serve the application: ایپلیکیشن کو سرو کرنا
- to serve the page: صفحہ سرو کرنا
- the app: ایپ
- the application: ایپلیکیشن
- the server: سرور
- the client: کلائنٹ
- the user: صارف
- the developer: ڈویلپر
- the browser: براؤزر
- the editor: ایڈیٹر
- the file: فائل
- the folder: فولڈر
- the directory: ڈائریکٹری
- the request: request
- the response: response
- the error response: error response
- the path operation: path operation
- the path operation decorator: path operation decorator
- the path operation function: path operation function
- the body: body
- the request body: request body
- the response body: response body
- the JSON body: JSON body
- the form body: form body
- the file body: file body
- the function body: function body
- the parameter: parameter
- the body parameter: body parameter
- the path parameter: path parameter
- the query parameter: query parameter
- the cookie parameter: cookie parameter
- the header parameter: header parameter
- the form parameter: form parameter
- the function parameter: function parameter
- the event: event
- the startup event: startup event
- the startup of the server: سرور کا startup
- the shutdown event: shutdown event
- the lifespan event: lifespan event
- the lifespan: lifespan
- the handler: handler
- the event handler: event handler
- the exception handler: exception handler
- to handle: سنبھالنا
- the model: model
- the Pydantic model: Pydantic model
- the data model: data model
- the database model: database model
- the form model: form model
- the model object: model object
- the class: class
- the base class: base class
- the parent class: parent class
- the subclass: subclass
- the child class: child class
- the sibling class: sibling class
- the class method: class method
- the header: header
- the headers: headers
- the authorization header: authorization header
- the `Authorization` header: `Authorization` header
- the forwarded header: forwarded header
- the dependency injection system: dependency injection system
- the dependency: dependency
- the dependable: dependable
- the dependant: dependant
- I/O bound: I/O bound
- CPU bound: CPU bound
- concurrency: concurrency
- parallelism: parallelism
- multiprocessing: multiprocessing
- async: async
- the coroutine: coroutine
- the env var: env var
- the environment variable: environment variable
- the virtual environment: virtual environment
- the `PATH`: `PATH`
- the `PATH` variable: `PATH` variable
- the authentication: authentication
- the authentication provider: authentication provider
- the authorization: authorization
- the authorization form: authorization form
- the authorization provider: authorization provider
- the user authenticates: صارف authenticate کرتا ہے
- the system authenticates the user: سسٹم صارف کو authenticate کرتا ہے
- the security: security
- the security scheme: security scheme
- the Bearer Token: Bearer Token
- the CLI: CLI
- the command line interface: command line interface
- the command: کمانڈ
- the cloud provider: cloud provider
- the cloud service: cloud service
- the deployment: deployment
- to deploy: deploy کرنا
- the development: ڈیولپمنٹ
- the development stages: ڈیولپمنٹ کے مراحل
- the dict: dict
- the dictionary: dictionary
- the enumeration: enumeration
- the enum: enum
- the enum member: enum member
- the string: string
- the list: list
- the encoder: encoder
- the decoder: decoder
- to encode: encode کرنا
- to decode: decode کرنا
- the exception: exception
- to raise: raise کرنا
- the expression: expression
- the statement: statement
- the type annotation: type annotation
- the type hint: type hint
- the return type: return type
- the return value: return value
- to return: واپس کرنا
- to validate: validate کرنا
- to import: import کرنا
- to declare: declare کرنا
- to install: انسٹال کرنا
- the frontend: frontend
- the backend: backend
- the GitHub discussion: GitHub discussion
- the GitHub issue: GitHub issue
- the pull request: pull request
- the commit: commit
- the breaking change: breaking change
- the bug: bug
- the performance: کارکردگی
- the performance optimization: کارکردگی کی optimization
- the task: task
- the background task: background task
- the task function: task function
- the template: template
- the template engine: template engine
- the server worker: server worker
- the Uvicorn worker: Uvicorn worker
- the Gunicorn Worker: Gunicorn Worker
- the worker process: worker process
- the worker class: worker class
- the workload: workload
- the SDK: SDK
- the software development kit: software development kit
- the `APIRouter`: `APIRouter`
- the `requirements.txt`: `requirements.txt`
- the button: بٹن
- the callable: callable
- the code: کوڈ
- the context manager: context manager
- the async context manager: async context manager
- the database session: database session
- the disk: ڈسک
- the domain: ڈومین
- the engine: engine
- the fake X: جعلی X
- the HTTP GET method: HTTP GET method
- the item: item
- the library: لائبریری
- the lock: lock
- the middleware: middleware
- the mobile application: موبائل ایپلیکیشن
- the module: module
- the mounting: mounting
- the network: نیٹ ورک
- the origin: origin
- the override: override
- the payload: payload
- the processor: پروسیسر
- the property: property
- the proxy: proxy
- the query: query
- the RAM: RAM
- the remote machine: ریموٹ مشین
- the status code: status code
- the tag: tag
- the web framework: ویب framework
- the framework: framework
- the endpoint: endpoint
- the plug-in: plug-in
- the wildcard: wildcard
- the feature: خصوصیت
- the guide: گائیڈ
- autocomplete: autocomplete
- autocompletion: autocompletion
- media type: media type
- cross origin: cross origin
- Cross-Origin Resource Sharing: Cross-Origin Resource Sharing

### Appendix: RTL stylesheet

The `<div dir="rtl">` wrapper and the per-block `<div dir="ltr">` wrappers exist because a translated markdown file cannot set attributes on the `<ul>`, `<pre>`, and `<h2>` elements that Markdown generates. If the build permits a language-specific stylesheet, these three rules do the same job for the whole site and let the wrappers be dropped:

```css
.md-typeset { direction: rtl; text-align: right; }
.md-typeset pre, .md-typeset code { direction: ltr; text-align: left; }
.md-typeset ul, .md-typeset ol { direction: rtl; }
```

Better still, Material for MkDocs supports right-to-left natively. Setting `direction: rtl` under `theme` in the generated `mkdocs.yml` for this language flips the navigation, sidebar, table of contents, and search box as well — none of which any in-document wrapper can reach.
