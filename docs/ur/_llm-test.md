<div dir="rtl" style="text-align: right;">

# LLM ٹیسٹ فائل { #llm-test-file }

یہ دستاویز جانچتی ہے کہ آیا وہ <abbr title="Large Language Model: بڑا لسانی ماڈل">LLM</abbr> ، جو documentation کا ترجمہ کرتا ہے، `scripts/translate.py` میں موجود `general_prompt` اور `docs/{language code}/llm-prompt.md` میں موجود زبان کے مخصوص prompt کو سمجھتا ہے یا نہیں۔ زبان کا مخصوص prompt ، `general_prompt` کے آخر میں جوڑا جاتا ہے۔

یہاں شامل کیے گئے tests زبان کے مخصوص prompts کے تمام ڈیزائنرز کو نظر آئیں گے۔

اسے یوں استعمال کریں**:**

* زبان کا ایک مخصوص prompt رکھیں - `docs/{language code}/llm-prompt.md` ۔
* اس دستاویز کا اپنی مطلوبہ ہدف زبان میں تازہ ترجمہ کریں (مثلاً `translate.py` کی `translate-page` command دیکھیں)۔ اس سے ترجمہ `docs/{language code}/docs/_llm-test.md` کے تحت بن جائے گا۔
* دیکھیں کہ ترجمے میں سب کچھ ٹھیک ہے یا نہیں۔
* اگر ضرورت ہو تو اپنے زبان کے مخصوص prompt ، general prompt ، یا انگریزی دستاویز کو بہتر بنائیں۔
* پھر ترجمے میں باقی رہ جانے والے مسائل کو دستی طور پر درست کریں، تاکہ یہ ایک اچھا ترجمہ بن جائے۔
* اچھا ترجمہ اپنی جگہ رکھتے ہوئے دوبارہ ترجمہ کریں۔ مثالی نتیجہ یہ ہو گا کہ LLM ترجمے میں مزید کوئی تبدیلی نہ کرے۔ اس کا مطلب ہے کہ general prompt اور آپ کا زبان کا مخصوص prompt اتنے ہی بہتر ہیں جتنے ہو سکتے ہیں (کبھی کبھار یہ چند بظاہر بے ترتیب تبدیلیاں کرے گا، اس کی وجہ یہ ہے کہ [LLMs متعین الگورتھم نہیں ہیں](https://doublespeak.chat/#/handbook#deterministic-output))۔

یہ رہے tests**:**

## Code snippets { #code-snippets }

//// tab | ٹیسٹ

یہ ایک code snippet ہے**:** `foo` ۔ اور یہ ایک اور code snippet ہے**:** `bar` ۔ اور ایک اور**:** `baz quux` ۔

////

//// tab | معلومات

code snippets کا مواد ویسا ہی رہنا چاہیے جیسا ہے۔

`scripts/translate.py` میں موجود general prompt کا حصہ `### Content of code snippets` دیکھیں۔

////

## واوین { #quotes }

//// tab | ٹیسٹ

کل میرے دوست نے لکھا**:** "اگر آپ "incorrectly" کے ہجے درست لکھ دیں، تو آپ نے اسے غلط لکھا ہے"۔ جس پر میں نے جواب دیا**:** "درست، لیکن 'incorrectly' غلط طور پر '"incorrectly"' نہیں ہے"۔

/// note | نوٹ

LLM شاید اس کا ترجمہ غلط کرے گا۔ دلچسپ بات صرف یہ ہے کہ آیا دوبارہ ترجمہ کرتے وقت وہ درست شدہ ترجمے کو برقرار رکھتا ہے یا نہیں۔

///

////

//// tab | معلومات

prompt ڈیزائنر یہ فیصلہ کر سکتا ہے کہ آیا وہ neutral واوین کو typographic واوین میں تبدیل کرنا چاہتا ہے۔ انہیں ویسا ہی چھوڑ دینا بھی ٹھیک ہے۔

مثال کے طور پر `docs/de/llm-prompt.md` میں حصہ `### Quotes` دیکھیں۔

////

## Code snippets میں واوین { #quotes-in-code-snippets }

//// tab | ٹیسٹ

`pip install "foo[bar]"`

code snippets میں string literals کی مثالیں**:** `"this"` ، `'that'` ۔

code snippets میں string literals کی ایک مشکل مثال**:** `f"I like {'oranges' if orange else "apples"}"`

مشکل ترین**:** `Yesterday, my friend wrote: "If you spell incorrectly correctly, you have spelled it incorrectly". To which I answered: "Correct, but 'incorrectly' is incorrectly not '"incorrectly"'"`

////

//// tab | معلومات

... تاہم، code snippets کے اندر واوین ویسے ہی رہنے چاہئیں۔

////

## code blocks { #code-blocks }

//// tab | ٹیسٹ

ایک Bash code کی مثال ...

```bash
# کائنات کے نام ایک سلام لکھیں
echo "Hello universe"
```

... اور ایک console code کی مثال ...

```console
$ <font color="#4E9A06">fastapi</font> run <u style="text-decoration-style:solid">main.py</u>
<span style="background-color:#009485"><font color="#D3D7CF"> FastAPI </font></span>  Starting server
        Searching for package file structure
```

... اور ایک اور console code کی مثال ...

```console
// ایک directory "Code" بنائیں
$ mkdir code
// اس directory میں جائیں
$ cd code
```

... اور ایک Python code کی مثال ...

```Python
wont_work()  # یہ کام نہیں کرے گا 😱
works(foo="bar")  # یہ کام کرتا ہے 🎉
```

... اور بس اتنا ہی۔

////

//// tab | معلومات

code blocks میں موجود code میں ترمیم نہیں ہونی چاہیے، سوائے تبصروں کے۔

`scripts/translate.py` میں موجود general prompt کا حصہ `### Content of code blocks` دیکھیں۔

////

## Tabs اور رنگین boxes { #tabs-and-colored-boxes }

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

Tabs اور `Info` / `Note` / `Warning` / وغیرہ blocks کے عنوان کا ترجمہ ایک عمودی لکیر (`|`) کے بعد شامل کیا جانا چاہیے۔

`scripts/translate.py` میں موجود general prompt کے حصے `### Special blocks` اور `### Tab blocks` دیکھیں۔

////

## ویب اور اندرونی links { #web-and-internal-links }

//// tab | ٹیسٹ

link کا متن ترجمہ ہونا چاہیے، link کا پتہ غیر تبدیل شدہ رہنا چاہیے**:**

* [اوپر والی سرخی کا link](#code-snippets)
* [اندرونی link](index.md#installation)
* [بیرونی link](https://sqlmodel.tiangolo.com/)
* [ایک style کا link](https://fastapi.tiangolo.com/css/styles.css)
* [ایک script کا link](https://fastapi.tiangolo.com/js/logic.js)
* [ایک image کا link](https://fastapi.tiangolo.com/img/foo.jpg)

link کا متن ترجمہ ہونا چاہیے، link کا پتہ ترجمے کی طرف اشارہ کرنا چاہیے**:**

* [FastAPI کا link](https://fastapi.tiangolo.com/ur/)

////

//// tab | معلومات

Links کا ترجمہ ہونا چاہیے، لیکن ان کا پتہ غیر تبدیل شدہ رہنا چاہیے۔ اس کی ایک استثنا FastAPI documentation کے صفحات کے مطلق links ہیں۔ اس صورت میں انہیں ترجمے کی طرف link کرنا چاہیے۔

`scripts/translate.py` میں موجود general prompt کا حصہ `### Links` دیکھیں۔

////

## HTML کے "abbr" elements { #html-abbr-elements }

//// tab | ٹیسٹ

یہاں کچھ چیزیں HTML کے "abbr" elements میں لپٹی ہوئی ہیں (کچھ فرضی ہیں)**:**

### abbr ایک مکمل جملہ دیتا ہے { #the-abbr-gives-a-full-phrase }

* <abbr title="Getting Things Done: کام نمٹانا">GTD</abbr>
* <abbr title="less than: اس سے کم"><code>lt</code></abbr>
* <abbr title="XML Web Token: ایکس ایم ایل ویب ٹوکن">XWT</abbr>
* <abbr title="Parallel Server Gateway Interface: متوازی سرور گیٹ وے انٹرفیس">PSGI</abbr>

### abbr ایک مکمل جملہ اور ایک وضاحت دیتا ہے { #the-abbr-gives-a-full-phrase-and-an-explanation }

* <abbr title="Mozilla Developer Network: ڈویلپرز کے لیے documentation ، جو Firefox والوں نے لکھی ہے">MDN</abbr>
* <abbr title="Input/Output: ڈسک سے پڑھنا یا اس پر لکھنا، نیٹ ورک کے رابطے۔">I/O</abbr> ۔

////

//// tab | معلومات

"abbr" elements کی "title" attributes کا ترجمہ کچھ مخصوص ہدایات کے مطابق کیا جاتا ہے۔

ترجمے اپنے "abbr" elements شامل کر سکتے ہیں جنہیں LLM کو نہیں ہٹانا چاہیے۔ مثلاً انگریزی الفاظ کی وضاحت کے لیے۔

`scripts/translate.py` میں موجود general prompt کا حصہ `### HTML abbr elements` دیکھیں۔

////

## HTML کے "dfn" elements { #html-dfn-elements }

* <dfn title="مشینوں کا ایک گروہ جنہیں اس طرح ترتیب دیا گیا ہو کہ وہ آپس میں جڑ کر کسی نہ کسی انداز میں مل کر کام کریں۔">cluster</dfn>
* <dfn title="مشین لرننگ کا ایک طریقہ جو مصنوعی نیورل نیٹ ورکس استعمال کرتا ہے جن میں input اور output کی تہوں کے درمیان بے شمار پوشیدہ تہیں ہوتی ہیں، اور یوں ایک جامع اندرونی ساخت تیار ہوتی ہے">Deep Learning</dfn>

## سرخیاں { #headings }

//// tab | ٹیسٹ

### ایک webapp بنائیں - ایک ٹیوٹوریل { #develop-a-webapp-a-tutorial }

السلام علیکم۔

### Type hints اور annotations { #type-hints-and-annotations }

ایک بار پھر السلام علیکم۔

### Superclasses اور subclasses { #super-and-subclasses }

ایک بار پھر السلام علیکم۔

////

//// tab | معلومات

سرخیوں کے لیے واحد سخت اصول یہ ہے کہ LLM ، خمدار قوسین کے اندر hash والے حصے کو غیر تبدیل شدہ چھوڑ دے، جس سے یہ یقینی بنتا ہے کہ links نہ ٹوٹیں۔

`scripts/translate.py` میں موجود general prompt کا حصہ `### Headings` دیکھیں۔

زبان کی کچھ مخصوص ہدایات کے لیے، مثلاً `docs/de/llm-prompt.md` میں حصہ `### Headings` دیکھیں۔

////

## docs میں استعمال ہونے والی اصطلاحات { #terms-used-in-the-docs }

//// tab | ٹیسٹ

* آپ
* آپ کا

* مثلاً
* وغیرہ

* `foo` بطور `int`
* `bar` بطور `str`
* `baz` بطور `list`

* ٹیوٹوریل - یوزر گائیڈ
* ایڈوانسڈ یوزر گائیڈ
* SQLModel کی docs
* API docs
* خودکار docs

* Data Science
* Deep Learning
* Machine Learning
* Dependency Injection
* HTTP Basic authentication
* HTTP Digest
* ISO format
* JSON Schema معیار
* JSON schema
* schema کی تعریف
* Password Flow
* موبائل

* deprecated
* ڈیزائن کیا گیا
* invalid
* موقع پر ہی
* معیاری
* ڈیفالٹ
* case-sensitive
* case-insensitive

* application کو سرو کرنا
* صفحہ سرو کرنا

* app
* application

* request
* response
* error response

* path operation
* path operation decorator
* path operation function

* body
* request body
* response body
* JSON body
* form body
* file body
* function body

* parameter
* body parameter
* path parameter
* query parameter
* cookie parameter
* header parameter
* form parameter
* function parameter

* event
* startup event
* server کا startup
* shutdown event
* lifespan event

* handler
* event handler
* exception handler
* سنبھالنا

* model
* Pydantic model
* data model
* database model
* form model
* model object

* class
* base class
* parent class
* subclass
* child class
* sibling class
* class method

* header
* headers
* authorization header
* `Authorization` header
* forwarded header

* dependency injection system
* dependency
* dependable
* dependant

* I/O bound
* CPU bound
* concurrency
* parallelism
* multiprocessing

* env var
* environment variable
* `PATH`
* `PATH` variable

* authentication
* authentication provider
* authorization
* authorization form
* authorization provider
* صارف authenticate کرتا ہے
* سسٹم صارف کو authenticate کرتا ہے

* CLI
* command line interface

* server
* client

* cloud provider
* cloud service

* ڈیولپمنٹ
* ڈیولپمنٹ کے مراحل

* dict
* dictionary
* enumeration
* enum
* enum member

* encoder
* decoder
* encode کرنا
* decode کرنا

* exception
* raise کرنا

* expression
* statement

* frontend
* backend

* GitHub discussion
* GitHub issue

* کارکردگی
* کارکردگی کی optimization

* return type
* return value

* security
* security scheme

* task
* background task
* task function

* template
* template engine

* type annotation
* type hint

* server worker
* Uvicorn worker
* Gunicorn Worker
* worker process
* worker class
* workload

* deployment
* deploy کرنا

* SDK
* software development kit

* `APIRouter`
* `requirements.txt`
* Bearer Token
* breaking change
* bug
* بٹن
* callable
* code
* commit
* context manager
* coroutine
* database session
* ڈسک
* domain
* engine
* جعلی X
* HTTP GET method
* item
* library
* lifespan
* lock
* middleware
* موبائل application
* module
* mounting
* نیٹ ورک
* origin
* override
* payload
* processor
* property
* proxy
* pull request
* query
* RAM
* ریموٹ مشین
* status code
* string
* tag
* web framework
* wildcard
* واپس کرنا
* validate کرنا

////

//// tab | معلومات

یہ docs میں نظر آنے والی (زیادہ تر) تکنیکی اصطلاحات کی نہ تو مکمل فہرست ہے اور نہ ہی معیاری۔ یہ prompt ڈیزائنر کے لیے یہ جاننے میں مددگار ہو سکتی ہے کہ کن اصطلاحات کے لیے LLM کو مدد کی ضرورت ہے۔ مثال کے طور پر جب وہ بار بار کسی اچھے ترجمے کو کم بہتر ترجمے میں بدل دیتا ہو۔ یا جب اسے آپ کی زبان میں کسی اصطلاح کی گردان یا اعراب میں مسئلہ ہو۔

مثلاً `docs/de/llm-prompt.md` میں حصہ `### List of English terms and their preferred German translations` دیکھیں۔

////

</div>
