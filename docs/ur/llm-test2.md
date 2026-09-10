<div dir="rtl" style="text-align: right;">

# ایل ایل ایم ٹیسٹ فائل { #llm-test-file }

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

```bash
# کائنات کے نام ایک سلام لکھیں
echo "Hello universe"
```

... اور ایک console کوڈ کی مثال ...

```console
$ <font color="#4E9A06">fastapi</font> run <u style="text-decoration-style:solid">main.py</u>
<span style="background-color:#009485"><font color="#D3D7CF"> FastAPI </font></span>  Starting server
        Searching for package file structure
```

... اور ایک اور console کوڈ کی مثال ...

```console
// ایک ڈائریکٹری "Code" بنائیں
$ mkdir code
// اس ڈائریکٹری میں جائیں
$ cd code
```

... اور ایک Python کوڈ کی مثال ...

```Python
wont_work()  # یہ کام نہیں کرے گا 😱
works(foo="bar")  # یہ کام کرتا ہے 🎉
```

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

## ایچ ٹی ایم ایل کے "abbr" عناصر { #html-abbr-elements }

//// tab | ٹیسٹ

یہاں کچھ چیزیں ایچ ٹی ایم ایل کے "abbr" عناصر میں لپٹی ہوئی ہیں (کچھ فرضی ہیں)**:**

### abbr مکمل فقرہ دیتا ہے { #the-abbr-gives-a-full-phrase }

* &rlm;<abbr title="Getting Things Done - کام نمٹانا">GTD</abbr>
* &rlm;<abbr title="less than - اس سے کم"><code>lt</code></abbr>
* &rlm;<abbr title="XML Web Token - ایکس ایم ایل ویب ٹوکن">XWT</abbr>
* &rlm;<abbr title="Parallel Server Gateway Interface - متوازی سرور گیٹ وے انٹرفیس">PSGI</abbr>

### abbr مکمل فقرہ اور وضاحت دیتا ہے { #the-abbr-gives-a-full-phrase-and-an-explanation }

* &rlm;<abbr title="Mozilla Developer Network - موزیلا ڈویلپر نیٹ ورک: ڈویلپرز کے لیے دستاویزات ، جو Firefox والوں نے لکھی ہیں">MDN</abbr>
* &rlm;<abbr title="Input/Output - ان پٹ / آؤٹ پٹ: ڈسک سے پڑھنا یا اس پر لکھنا، نیٹ ورک کے رابطے۔">I/O</abbr> ۔

////

//// tab | معلومات

"abbr" عناصر کی "title" attributes کا ترجمہ کچھ مخصوص ہدایات کے مطابق کیا جاتا ہے۔

ترجمے اپنے "abbr" عناصر شامل کر سکتے ہیں جنہیں LLM کو نہیں ہٹانا چاہیے۔ مثلاً انگریزی الفاظ کی وضاحت کے لیے۔

`scripts/translate.py` میں موجود عمومی prompt کا حصہ `### HTML abbr elements` دیکھیں۔

////

## ایچ ٹی ایم ایل کے "dfn" عناصر { #html-dfn-elements }

* &rlm;<dfn title="مشینوں کا ایک گروہ جنہیں اس طرح ترتیب دیا گیا ہو کہ وہ آپس میں جڑ کر کسی نہ کسی انداز میں مل کر کام کریں۔">cluster</dfn>
* &rlm;<dfn title="مشین لرننگ کا ایک طریقہ جو مصنوعی نیورل نیٹ ورکس استعمال کرتا ہے، جن میں ان پٹ اور آؤٹ پٹ کی تہوں کے درمیان بے شمار پوشیدہ تہیں ہوتی ہیں، اور یوں ایک جامع اندرونی ساخت تیار ہوتی ہے">Deep Learning</dfn>

## سرخیاں { #headings }

//// tab | ٹیسٹ

### ویب ایپ بنائیں - ایک ٹیوٹوریل { #develop-a-webapp-a-tutorial }

السلام علیکم۔

### ٹائپ ہنٹس اور اینوٹیشنز { #type-hints-and-annotations }

ایک بار پھر السلام علیکم۔

### سُپر کلاسز اور سب کلاسز { #super-and-subclasses }

ایک بار پھر السلام علیکم۔

////

//// tab | معلومات

سرخیوں کے لیے واحد سخت اصول یہ ہے کہ LLM ، خمدار قوسین کے اندر hash والے حصے کو غیر تبدیل شدہ چھوڑ دے، جس سے یہ یقینی بنتا ہے کہ لنکس نہ ٹوٹیں۔

`scripts/translate.py` میں موجود عمومی prompt کا حصہ `### Headings` دیکھیں۔

زبان کی کچھ مخصوص ہدایات کے لیے، مثلاً `docs/de/llm-prompt.md` میں حصہ `### Headings` دیکھیں۔

////

## دستاویزات میں استعمال ہونے والی اصطلاحات { #terms-used-in-the-docs }

//// tab | ٹیسٹ

* آپ
* آپ کا

* مثلاً
* وغیرہ

* &rlm;`foo` بطور `int`
* &rlm;`bar` بطور `str`
* &rlm;`baz` بطور `list`

* ٹیوٹوریل - یوزر گائیڈ
* ایڈوانسڈ یوزر گائیڈ
* &rlm;SQLModel کی دستاویزات
* &rlm;API دستاویزات
* خودکار دستاویزات

* ڈیٹا سائنس
* ڈیپ لرننگ
* مشین لرننگ
* &rlm;Dependency Injection
* &rlm;HTTP Basic authentication
* &rlm;HTTP Digest
* &rlm;ISO format
* &rlm;JSON Schema معیار
* &rlm;JSON schema
* &rlm;schema کی تعریف
* &rlm;Password Flow
* موبائل

* &rlm;deprecated
* ڈیزائن کیا گیا
* غلط
* موقع پر ہی
* معیاری
* ڈیفالٹ
* &rlm;case-sensitive
* &rlm;case-insensitive

* ایپلیکیشن کو سرو کرنا
* صفحہ سرو کرنا

* ایپ
* ایپلیکیشن

* &rlm;request
* &rlm;response
* &rlm;error response

* &rlm;path operation
* &rlm;path operation decorator
* &rlm;path operation function

* &rlm;body
* &rlm;request body
* &rlm;response body
* &rlm;JSON body
* &rlm;form body
* &rlm;file body
* &rlm;function body

* &rlm;parameter
* &rlm;body parameter
* &rlm;path parameter
* &rlm;query parameter
* &rlm;cookie parameter
* &rlm;header parameter
* &rlm;form parameter
* &rlm;function parameter

* &rlm;event
* &rlm;startup event
* سرور کا startup
* &rlm;shutdown event
* &rlm;lifespan event

* &rlm;handler
* &rlm;event handler
* &rlm;exception handler
* سنبھالنا

* &rlm;model
* &rlm;Pydantic model
* &rlm;data model
* &rlm;database model
* &rlm;form model
* &rlm;model object

* &rlm;class
* &rlm;base class
* &rlm;parent class
* &rlm;subclass
* &rlm;child class
* &rlm;sibling class
* &rlm;class method

* &rlm;header
* &rlm;headers
* &rlm;authorization header
* &rlm;`Authorization` header
* &rlm;forwarded header

* &rlm;dependency injection system
* &rlm;dependency
* &rlm;dependable
* &rlm;dependant

* &rlm;I/O bound
* &rlm;CPU bound
* &rlm;concurrency
* &rlm;parallelism
* &rlm;multiprocessing

* &rlm;env var
* &rlm;environment variable
* &rlm;`PATH`
* &rlm;`PATH` variable

* &rlm;authentication
* &rlm;authentication provider
* &rlm;authorization
* &rlm;authorization form
* &rlm;authorization provider
* صارف authenticate کرتا ہے
* سسٹم صارف کو authenticate کرتا ہے

* &rlm;CLI
* کمانڈ لائن انٹرفیس

* سرور
* کلائنٹ

* کلاؤڈ فراہم کنندہ
* کلاؤڈ سروس

* ڈیولپمنٹ
* ڈیولپمنٹ کے مراحل

* &rlm;dict
* &rlm;dictionary
* &rlm;enumeration
* &rlm;enum
* &rlm;enum member

* &rlm;encoder
* &rlm;decoder
* &rlm;encode کرنا
* &rlm;decode کرنا

* &rlm;exception
* &rlm;raise کرنا

* &rlm;expression
* &rlm;statement

* &rlm;frontend
* &rlm;backend

* &rlm;GitHub discussion
* &rlm;GitHub issue

* کارکردگی
* کارکردگی کی optimization

* &rlm;return type
* &rlm;return value

* &rlm;security
* &rlm;security scheme

* &rlm;task
* &rlm;background task
* &rlm;task function

* &rlm;template
* &rlm;template engine

* &rlm;type annotation
* &rlm;type hint

* &rlm;server worker
* &rlm;Uvicorn worker
* &rlm;Gunicorn Worker
* &rlm;worker process
* &rlm;worker class
* &rlm;workload

* &rlm;deployment
* &rlm;deploy کرنا

* &rlm;SDK
* سافٹ ویئر ڈیولپمنٹ کٹ

* &rlm;`APIRouter`
* &rlm;`requirements.txt`
* &rlm;Bearer Token
* &rlm;breaking change
* &rlm;bug
* بٹن
* &rlm;callable
* کوڈ
* &rlm;commit
* &rlm;context manager
* &rlm;coroutine
* &rlm;database session
* ڈسک
* ڈومین
* &rlm;engine
* جعلی X
* &rlm;HTTP GET method
* &rlm;item
* لائبریری
* &rlm;lifespan
* &rlm;lock
* &rlm;middleware
* موبائل ایپلیکیشن
* &rlm;module
* &rlm;mounting
* نیٹ ورک
* &rlm;origin
* &rlm;override
* &rlm;payload
* پروسیسر
* &rlm;property
* &rlm;proxy
* &rlm;pull request
* &rlm;query
* &rlm;RAM
* ریموٹ مشین
* &rlm;status code
* &rlm;string
* &rlm;tag
* ویب framework
* &rlm;wildcard
* واپس کرنا
* &rlm;validate کرنا

////

//// tab | معلومات

یہ دستاویزات میں نظر آنے والی (زیادہ تر) تکنیکی اصطلاحات کی نہ تو مکمل فہرست ہے اور نہ ہی معیاری۔ یہ prompt ڈیزائنر کے لیے یہ جاننے میں مددگار ہو سکتی ہے کہ کن اصطلاحات کے لیے LLM کو مدد کی ضرورت ہے۔ مثال کے طور پر جب وہ بار بار کسی اچھے ترجمے کو کم بہتر ترجمے میں بدل دیتا ہو۔ یا جب اسے آپ کی زبان میں کسی اصطلاح کی گردان یا اعراب میں مسئلہ ہو۔

مثلاً `docs/de/llm-prompt.md` میں حصہ `### List of English terms and their preferred German translations` دیکھیں۔

////

</div>
