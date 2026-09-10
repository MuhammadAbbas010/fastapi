<div dir="rtl" style="text-align: right;">

# &rlm;LLM ٹیسٹ فائل { #llm-test-file }

یہ دستاویز جانچتی ہے کہ آیا وہ <abbr title="Large Language Model - بڑا لسانی ماڈل">LLM</abbr> ، جو دستاویزات کا ترجمہ کرتا ہے، `scripts/translate.py` میں موجود `general_prompt` اور `docs/{language code}/llm-prompt.md` میں موجود زبان کے مخصوص prompt کو سمجھتا ہے یا نہیں۔ زبان کا مخصوص prompt ، `general_prompt` کے آخر میں جوڑ دیا جاتا ہے۔

یہاں شامل کیے گئے ٹیسٹ زبان کے مخصوص prompts کے تمام ڈیزائنرز کو نظر آئیں گے۔

اسے یوں استعمال کریں**:**

* زبان کا ایک مخصوص prompt رکھیں - `docs/{language code}/llm-prompt.md` ۔
* اس دستاویز کا اپنی مطلوبہ ہدف زبان میں تازہ ترجمہ کریں (مثلاً `translate.py` کی `translate-page` کمانڈ دیکھیں)۔ اس سے ترجمہ `docs/{language code}/docs/_llm-test.md` کے تحت بن جائے گا۔
* دیکھیں کہ ترجمے میں سب کچھ ٹھیک ہے یا نہیں۔
* اگر ضرورت ہو تو اپنے زبان کے مخصوص prompt ، عمومی prompt ، یا انگریزی دستاویز کو بہتر بنائیں۔
* پھر ترجمے میں باقی رہ جانے والے مسائل دستی طور پر درست کریں، تاکہ یہ ایک اچھا ترجمہ بن جائے۔
* اچھا ترجمہ اپنی جگہ رکھتے ہوئے دوبارہ ترجمہ کریں۔ مثالی نتیجہ یہ ہو گا کہ LLM ترجمے میں مزید کوئی تبدیلی نہ کرے۔ اس کا مطلب ہے کہ عمومی prompt اور آپ کا زبان کا مخصوص prompt اتنے ہی بہتر ہیں جتنے ہو سکتے ہیں (کبھی کبھار یہ چند بظاہر بے ترتیب تبدیلیاں کرے گا، اس کی وجہ یہ ہے کہ [LLMs متعین الگورتھم نہیں ہیں](https://doublespeak.chat/#/handbook#deterministic-output))۔

یہ رہے ٹیسٹ**:**

## کوڈ کے ٹکڑے { #code-snippets }

//// tab | ٹیسٹ

یہ ایک کوڈ کا ٹکڑا ہے**:** `foo` ۔ اور یہ ایک اور کوڈ کا ٹکڑا ہے**:** `bar` ۔ اور ایک اور**:** `baz quux` ۔

////

//// tab | معلومات

کوڈ کے ٹکڑوں کا مواد ویسا ہی رہنا چاہیے جیسا ہے۔

`scripts/translate.py` میں موجود عمومی prompt کا حصہ `### Content of code snippets` دیکھیں۔

////

## واوین { #quotes }

//// tab | ٹیسٹ

کل میرے دوست نے لکھا**:** "اگر آپ "incorrectly" کے ہجے درست لکھ دیں، تو آپ نے اسے غلط لکھا ہے۔" جس پر میں نے جواب دیا**:** "درست، لیکن 'incorrectly' غلط طور پر '"incorrectly"' نہیں ہے۔"

/// note | نوٹ

LLM شاید اس کا ترجمہ غلط کرے گا۔ دلچسپ بات صرف یہ ہے کہ آیا دوبارہ ترجمہ کرتے وقت وہ درست شدہ ترجمے کو برقرار رکھتا ہے یا نہیں۔

///

////

//// tab | معلومات

prompt ڈیزائنر یہ فیصلہ کر سکتا ہے کہ آیا وہ سادہ واوین کو طباعتی واوین میں بدلنا چاہتا ہے۔ انہیں ویسا ہی چھوڑ دینا بھی ٹھیک ہے۔

مثال کے طور پر `docs/de/llm-prompt.md` میں حصہ `### Quotes` دیکھیں۔

////

## کوڈ کے ٹکڑوں میں واوین { #quotes-in-code-snippets }

//// tab | ٹیسٹ

`pip install "foo[bar]"`

کوڈ کے ٹکڑوں میں string literals کی مثالیں**:** `"this"` ، `'that'` ۔

کوڈ کے ٹکڑوں میں string literals کی ایک مشکل مثال**:** `f"I like {'oranges' if orange else "apples"}"`

مشکل ترین**:** `Yesterday, my friend wrote: "If you spell incorrectly correctly, you have spelled it incorrectly". To which I answered: "Correct, but 'incorrectly' is incorrectly not '"incorrectly"'"`

////

//// tab | معلومات

... تاہم، کوڈ کے ٹکڑوں کے اندر واوین ویسے ہی رہنے چاہئیں۔

////

## کوڈ بلاکس { #code-blocks }

//// tab | ٹیسٹ

ایک Bash کوڈ کی مثال ...

<div dir="ltr">

```bash
# کائنات کے نام ایک سلام لکھیں
echo "Hello universe"
```

</div>

... اور ایک console کوڈ کی مثال ...

<div dir="ltr">

```console
$ <font color="#4E9A06">fastapi</font> run <u style="text-decoration-style:solid">main.py</u>
<span style="background-color:#009485"><font color="#D3D7CF"> FastAPI </font></span>  Starting server
        Searching for package file structure
```

</div>

... اور ایک اور console کوڈ کی مثال ...

<div dir="ltr">

```console
// ایک ڈائریکٹری "Code" بنائیں
$ mkdir code
// اس ڈائریکٹری میں جائیں
$ cd code
```

</div>

... اور ایک Python کوڈ کی مثال ...

<div dir="ltr">

```Python
wont_work()  # یہ کام نہیں کرے گا 😱
works(foo="bar")  # یہ کام کرتا ہے 🎉
```

</div>

... اور بس اتنا ہی۔

////

//// tab | معلومات

کوڈ بلاکس میں موجود کوڈ میں ترمیم نہیں ہونی چاہیے، سوائے تبصروں کے۔

`scripts/translate.py` میں موجود عمومی prompt کا حصہ `### Content of code blocks` دیکھیں۔

////

## ٹیبز اور رنگین ڈبے { #tabs-and-colored-boxes }

//// tab | ٹیسٹ

/// note | نوٹ
کچھ متن
///

/// note | تکنیکی تفصیلات
کچھ متن
///

/// tip | مشورہ
کچھ متن
///

/// warning | انتباہ
کچھ متن
///

/// danger | خطرہ
کچھ متن
///

////

//// tab | معلومات

ٹیبز اور `Info` / `Note` / `Warning` / وغیرہ بلاکس کے عنوان کا ترجمہ ایک عمودی لکیر (`|`) کے بعد شامل کیا جانا چاہیے۔

`scripts/translate.py` میں موجود عمومی prompt کے حصے `### Special blocks` اور `### Tab blocks` دیکھیں۔

////

## ویب اور اندرونی لنکس { #web-and-internal-links }

//// tab | ٹیسٹ

لنک کا متن ترجمہ ہونا چاہیے، لنک کا پتہ غیر تبدیل شدہ رہنا چاہیے**:**

* [اوپر والی سرخی کا لنک](#code-snippets)
* [اندرونی لنک](index.md#installation)
* [بیرونی لنک](https://sqlmodel.tiangolo.com/)
* [ایک style کا لنک](https://fastapi.tiangolo.com/css/styles.css)
* [ایک script کا لنک](https://fastapi.tiangolo.com/js/logic.js)
* [ایک تصویر کا لنک](https://fastapi.tiangolo.com/img/foo.jpg)

لنک کا متن ترجمہ ہونا چاہیے، لنک کا پتہ ترجمے کی طرف اشارہ کرنا چاہیے**:**

* [FastAPI کا لنک](https://fastapi.tiangolo.com/ur/)

////

//// tab | معلومات

لنکس کا ترجمہ ہونا چاہیے، لیکن ان کا پتہ غیر تبدیل شدہ رہنا چاہیے۔ اس کی ایک استثنا FastAPI دستاویزات کے صفحات کے مطلق لنکس ہیں۔ اس صورت میں انہیں ترجمے کی طرف لنک کرنا چاہیے۔

`scripts/translate.py` میں موجود عمومی prompt کا حصہ `### Links` دیکھیں۔

////

## &rlm;HTML کے "abbr" عناصر { #html-abbr-elements }

//// tab | ٹیسٹ

یہاں کچھ چیزیں HTML کے "abbr" عناصر میں لپٹی ہوئی ہیں (کچھ فرضی ہیں)**:**

### &rlm;abbr مکمل فقرہ دیتا ہے { #the-abbr-gives-a-full-phrase }

* <abbr title="Getting Things Done - کام نمٹانا">GTD</abbr>
* <abbr title="less than - اس سے کم"><code>lt</code></abbr>
* <abbr title="XML Web Token - ایکس ایم ایل ویب ٹوکن">XWT</abbr>
* <abbr title="Parallel Server Gateway Interface - متوازی سرور گیٹ وے انٹرفیس">PSGI</abbr>

### &rlm;abbr مکمل فقرہ اور وضاحت دیتا ہے { #the-abbr-gives-a-full-phrase-and-an-explanation }

* <abbr title="Mozilla Developer Network - موزیلا ڈویلپر نیٹ ورک: ڈویلپرز کے لیے دستاویزات ، جو Firefox والوں نے لکھی ہیں">MDN</abbr>
* <abbr title="Input/Output - ان پٹ / آؤٹ پٹ: ڈسک سے پڑھنا یا اس پر لکھنا، نیٹ ورک کے رابطے۔">I/O</abbr> ۔

////

//// tab | معلومات

"abbr" عناصر کی "title" attributes کا ترجمہ کچھ مخصوص ہدایات کے مطابق کیا جاتا ہے۔

ترجمے اپنے "abbr" عناصر شامل کر سکتے ہیں جنہیں LLM کو نہیں ہٹانا چاہیے۔ مثلاً انگریزی الفاظ کی وضاحت کے لیے۔

`scripts/translate.py` میں موجود عمومی prompt کا حصہ `### HTML abbr elements` دیکھیں۔

////

## &rlm;HTML کے "dfn" عناصر { #html-dfn-elements }

* <dfn title="مشینوں کا ایک گروہ جنہیں اس طرح ترتیب دیا گیا ہو کہ وہ آپس میں جڑ کر کسی نہ کسی انداز میں مل کر کام کریں۔">cluster</dfn>
* <dfn title="مشین لرننگ کا ایک طریقہ جو مصنوعی نیورل نیٹ ورکس استعمال کرتا ہے، جن میں ان پٹ اور آؤٹ پٹ کی تہوں کے درمیان بے شمار پوشیدہ تہیں ہوتی ہیں، اور یوں ایک جامع اندرونی ساخت تیار ہوتی ہے">Deep Learning</dfn>

## سرخیاں { #headings }

//// tab | ٹیسٹ

### ویب ایپ بنائیں - ایک ٹیوٹوریل { #develop-a-webapp-a-tutorial }

السلام علیکم۔

### &rlm;Type hints اور annotations { #type-hints-and-annotations }

ایک بار پھر السلام علیکم۔

### &rlm;Superclasses اور subclasses { #super-and-subclasses }

ایک بار پھر السلام علیکم۔

////

//// tab | معلومات

سرخیوں کے لیے واحد سخت اصول یہ ہے کہ LLM ، خمدار قوسین کے اندر hash والے حصے کو غیر تبدیل شدہ چھوڑ دے، جس سے یہ یقینی بنتا ہے کہ لنکس نہ ٹوٹیں۔

`scripts/translate.py` میں موجود عمومی prompt کا حصہ `### Headings` دیکھیں۔

زبان کی کچھ مخصوص ہدایات کے لیے، مثلاً `docs/de/llm-prompt.md` میں حصہ `### Headings` دیکھیں۔

////

## دستاویزات میں استعمال ہونے والی اصطلاحات { #terms-used-in-the-docs }

//// tab | ٹیسٹ

* you — آپ
* your — آپ کا

* e.g. — مثلاً
* etc. — وغیرہ

* `foo` as an `int` — `foo` بطور `int`
* `bar` as a `str` — `bar` بطور `str`
* `baz` as a `list` — `baz` بطور `list`

* the Tutorial - User guide — ٹیوٹوریل - یوزر گائیڈ
* the Advanced User Guide — ایڈوانسڈ یوزر گائیڈ
* the SQLModel docs — SQLModel کی دستاویزات
* the API docs — API دستاویزات
* the automatic docs — خودکار دستاویزات

* Data Science
* Deep Learning
* Machine Learning
* Dependency Injection
* HTTP Basic authentication
* HTTP Digest
* ISO format
* the JSON Schema standard — JSON Schema معیار
* the JSON schema — JSON schema
* the schema definition — schema کی تعریف
* Password Flow
* Mobile — موبائل

* deprecated — متروک
* designed — ڈیزائن کیا گیا
* invalid — غلط
* on the fly — موقع پر ہی
* standard — معیاری
* default — ڈیفالٹ
* case-sensitive
* case-insensitive

* to serve the application — ایپلیکیشن کو سرو کرنا
* to serve the page — صفحہ سرو کرنا

* the app — ایپ
* the application — ایپلیکیشن

* the request
* the response
* the error response

* the path operation
* the path operation decorator
* the path operation function

* the body
* the request body
* the response body
* the JSON body
* the form body
* the file body
* the function body

* the parameter
* the body parameter
* the path parameter
* the query parameter
* the cookie parameter
* the header parameter
* the form parameter
* the function parameter

* the event
* the startup event
* the startup of the server — سرور کا startup
* the shutdown event
* the lifespan event

* the handler
* the event handler
* the exception handler
* to handle — سنبھالنا

* the model
* the Pydantic model
* the data model
* the database model
* the form model
* the model object

* the class
* the base class
* the parent class
* the subclass
* the child class
* the sibling class
* the class method

* the header
* the headers
* the authorization header
* the `Authorization` header
* the forwarded header

* the dependency injection system
* the dependency
* the dependable
* the dependant

* I/O bound
* CPU bound
* concurrency
* parallelism
* multiprocessing

* the env var
* the environment variable
* the `PATH`
* the `PATH` variable

* the authentication
* the authentication provider
* the authorization
* the authorization form
* the authorization provider
* the user authenticates — صارف authenticate کرتا ہے
* the system authenticates the user — سسٹم صارف کو authenticate کرتا ہے

* the CLI
* the command line interface

* the server — سرور
* the client — کلائنٹ

* the cloud provider
* the cloud service

* the development — ڈیولپمنٹ
* the development stages — ڈیولپمنٹ کے مراحل

* the dict
* the dictionary
* the enumeration
* the enum
* the enum member

* the encoder
* the decoder
* to encode — encode کرنا
* to decode — decode کرنا

* the exception
* to raise — raise کرنا

* the expression
* the statement

* the frontend
* the backend

* the GitHub discussion
* the GitHub issue

* the performance — کارکردگی
* the performance optimization — کارکردگی کی optimization

* the return type
* the return value

* the security
* the security scheme

* the task
* the background task
* the task function

* the template
* the template engine

* the type annotation
* the type hint

* the server worker
* the Uvicorn worker
* the Gunicorn Worker
* the worker process
* the worker class
* the workload

* the deployment
* to deploy — deploy کرنا

* the SDK
* the software development kit

* the `APIRouter`
* the `requirements.txt`
* the Bearer Token
* the breaking change
* the bug
* the button — بٹن
* the callable
* the code — کوڈ
* the commit
* the context manager
* the coroutine
* the database session
* the disk — ڈسک
* the domain — ڈومین
* the engine
* the fake X — جعلی X
* the HTTP GET method
* the item
* the library — لائبریری
* the lifespan
* the lock
* the middleware
* the mobile application — موبائل ایپلیکیشن
* the module
* the mounting
* the network — نیٹ ورک
* the origin
* the override
* the payload
* the processor — پروسیسر
* the property
* the proxy
* the pull request
* the query
* the RAM
* the remote machine — ریموٹ مشین
* the status code
* the string
* the tag
* the web framework — ویب framework
* the wildcard
* to return — واپس کرنا
* to validate — validate کرنا

////

//// tab | معلومات

یہ دستاویزات میں نظر آنے والی (زیادہ تر) تکنیکی اصطلاحات کی نہ تو مکمل فہرست ہے اور نہ ہی معیاری۔ یہ prompt ڈیزائنر کے لیے یہ جاننے میں مددگار ہو سکتی ہے کہ کن اصطلاحات کے لیے LLM کو مدد کی ضرورت ہے۔ مثال کے طور پر جب وہ بار بار کسی اچھے ترجمے کو کم بہتر ترجمے میں بدل دیتا ہو۔ یا جب اسے آپ کی زبان میں کسی اصطلاح کی گردان یا اعراب میں مسئلہ ہو۔

مثلاً `docs/de/llm-prompt.md` میں حصہ `### List of English terms and their preferred German translations` دیکھیں۔

////

</div>
