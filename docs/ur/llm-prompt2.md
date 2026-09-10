### Target language

Translate to Urdu (اردو).

Language code: ur.

Keep existing translations as they are if the term is already translated. Only change an existing translation if it contradicts a rule below.

Only keep parentheses if they exist in the source text. Do not add parentheses to terms that do not have them.

### Script and Alignment

* Use Arabic script (Nastaliq) for Urdu text.
* Wrap the translated body in `<div dir="rtl" style="text-align: right;">...</div>` so headings, paragraphs, and lists render right-aligned. Leave a blank line after the opening tag and before the closing tag.
* Where an English/Latin-script term sits directly next to Urdu text, add one extra space around it, so the two scripts don't visually run together.
* When a line inside the RTL block begins with a Latin-script word, a backtick, or a digit, prefix the line content with `&rlm;` (U+200F). Without it the bidi algorithm takes the line's base direction from that first Latin character and lays the whole line out left-to-right, pushing the bullet and the English term to the left edge while the Urdu text sits at the right edge.

Example:

```
* &rlm;`foo` بطور `int`
* &rlm;`APIRouter`
* اصطلاحات
```

* Code blocks sit inside the RTL flow, so the block itself is aligned to the right side of the content column. Do not add `dir="ltr"` to a code block and do not move it out of the wrapper — this applies whether or not the block contains a translated Urdu comment.
* The characters inside a code block are still laid out left-to-right, because indentation, operators, and string literals are not meaningful right-to-left. To right-align the code text itself as well, that is a CSS change in `docs/ur/docs/css/custom.css`, not something the translation can express.

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
* Translate the whole heading into Urdu. Do not leave a heading half-English.
* Where the Urdu translation is a casual, everyday word, use the translation: `Headings` → `سرخیاں`, `Quotes` → `واوین`.
* Where no everyday Urdu word exists, transliterate rather than leaving the Latin word standing alone in an otherwise Urdu heading: `LLM` → `ایل ایل ایم`, `HTML` → `ایچ ٹی ایم ایل`, `Type hints` → `ٹائپ ہنٹس`.
* Keep the English word only where it is a proper noun or a product name and transliterating it would obscure it: `FastAPI`, `Pydantic`, `OpenAPI`, `Starlette`, `Python`.
* Keep literal identifiers as identifiers: an HTML tag name like `abbr`, a class name like `APIRouter`, a filename like `main.py`.
* Headings are inside the RTL wrapper, so the entire heading aligns right.

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
- Data Science: ڈیٹا سائنس
- Deep Learning: ڈیپ لرننگ
- Machine Learning: مشین لرننگ
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
- the virtual environment: ورچوئل انوائرمنٹ
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
- the command line interface: کمانڈ لائن انٹرفیس
- the command: کمانڈ
- the cloud provider: کلاؤڈ فراہم کنندہ
- the cloud service: کلاؤڈ سروس
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
- the software development kit: سافٹ ویئر ڈیولپمنٹ کٹ
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
- autocomplete: آٹو کمپلیٹ
- autocompletion: آٹو کمپلیشن
- media type: media type
- cross origin: cross origin
- Cross-Origin Resource Sharing: Cross-Origin Resource Sharing
