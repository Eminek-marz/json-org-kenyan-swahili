# JSON.org Specification (Kenyan Swahili Edition) 🇰🇪
> **Tafsiri Rasmi ya [json.org](https://www.json.org/) kwa Kiswahili cha Kawaida cha Kenya — Bila "Deep Translation".**
> *(Kulingana na Standard ya Kimataifa ya [ECMA-404: The JSON Data Interchange Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/))*

---

## Utangulizi wa JSON (Introducing JSON) 📄

**JSON** (JavaScript Object Notation) ni lightweight data-interchange format. Ni rahisi sana kwa mtu kusoma na kuandika JSON, na pia ni rahisi kwa mashine (computers) kui-parse na kui-generate. 

JSON ni subset ya **JavaScript Programming Language Standard (ECMA-262 3rd Edition - December 1999)**. 

JSON ni text format ambayo haitegemei programming language yoyote (**completely language independent**), lakini inatumia styles and rules (conventions) zinazofahamika virahisi na language programmers za **C-family** (kama vile C, C++, C#, Java, JavaScript, Perl, Python, na zingine nyingi). kwa sababu ya hiyo zinaifanya JSON kuwa language bora zaidi kwa kutransfer data kati ya mifumo tofauti (ideal data-interchange language).

---

## 1. Structures Mbili za Msingi za JSON 🧱

JSON imejengwa juu ya structures mbili pekee ambazo ni universal (zinapatikana kwa kila language duniani):

1. **Collection of name/value pairs**: 
   Kwa different programming languages, hii structure inafahamika kama ***object***, record, struct, dictionary, hash table, keyed list, au associative array.
2. **Ordered list of values**: 
   Kwa programming languages nyingi, hii structure inafahamika kama ***array***, vector, list, au sequence.

Hizi ni universal data structures. Karibu programming languages zote za kisasa zinazisupport in one way or the other. Kwa hivyo inamake sense kabisa kwamba data format inayotumiwa kusafirisha data kati ya languages tofauti pia ijengwe juu ya structures hizi hizi mbili.

---

## 2. JSON Forms & Syntax 📐

Ndani ya JSON, data inachukua mifumo hii:

### a) Object `{}`
*Object* ni unordered collection (unordered set) ya **name/value pairs**. 

* Object inaanza na **`{`** *(left brace)* na inaishia na **`}`** *(right brace)*.
* Kila jina (key) inafuatiwa na alama ya **`:`** *(colon)*.
* Hizo name/value pairs zinasaparestiwa kwa kutumia  **`,`** *(comma)*.

![JSON Object Diagram](https://www.json.org/img/object.png)

```json
{
  "name": "Nairobi Tech Hub",
  "city": "Nairobi",
  "established": 2024,
  "isActive": true
}
```

---

### b) Array `[]`
*Array* ni collection iliyopangwa (ordered collection) ya **values**. 

* Array inaanza na **`[`** *(left bracket)* na inaishia na **`]`** *(right bracket)*.
* Values zote ndani yake zinasaparestiwa na **`,`** *(comma)*.

![JSON Array Diagram](https://www.json.org/img/array.png)

```json
[
  "Sauti Sol",
  "Nyashinski",
  "Khaligraph Jones"
]
```

---

### c) Value (Thamani Inayoruhusiwa) 💎
Ndani ya JSON, **value** inaweza kuwa:
* **`string`** (ndani ya double quotes `""`)
* **`number`**
* **`true`** au **`false`** (boolean)
* **`null`** (Empty Debe)
* **`object`**
* **`array`**

Structures hizi zinaweza kuwekwa ndani ya nyingine (nested) kwa kiwango chochote unachotaka.

![JSON Value Diagram](https://www.json.org/img/value.png)

---

### d) String (Maandishi) 🔤
*String* ni sequence ya letters either zero  au zaidi za **Unicode**, zikiwa zimeenclosiwa ndani ya **double quotes `""`**, zikitumia backslash escapes. 

Letter moja inawakilishwa kama single character string. String ya JSON inafanana sana na string ya C au Java:

![JSON String Diagram](https://www.json.org/img/string.png)

#### Escape Characters Zinazoruhusiwa:
* `\"` — Quotation mark
* `\\` — Reverse solidus (backslash)
* `\/` — Solidus (slash)
* `\b` — Backspace
* `\f` — Formfeed
* `\n` — Newline (mstari mpya)
* `\r` — Carriage return
* `\t` — Tab
* `\u` ikifuatiwa na tarakimu 4 za hexadecimal (kwa mfano `\u0020`)

---

### e) Number 🔢
*Number* inafanana sana na namba ya kawaida ya C au Java, isipokuwa number system ya **octal** na **hexadecimal** haitumiwi hapa:

![JSON Number Diagram](https://www.json.org/img/number.png)

* Inaweza kuwa **integer** ya kawaida (mfano: `254`, `-10`).
* Inaweza kuwa na **decimal / fraction** (mfano: `850.50`).
* Inaweza kuwa na **exponent** kwa namba za kisayansi (mfano: `1.5e3`, `2E+10`).

---

### f) Whitespace ␣
Whitespace (nafasi tupu) kama vile **space**, **tab**, **newline**, au **carriage return** zinaweza kuwekwa katikati ya token yoyote bila kubadilisha maana ya data. 

Hii inamaanisha unaweza ku-format JSON yako iwe na mistari mizuri (pretty-printed) au iwe kwa mstari mmoja (minified) ili kusafiri haraka mtandaoni.

![JSON Whitespace Diagram](https://www.json.org/img/whitespace.png)

---

## 3. Grammar Rasmi ya JSON (McKeeman Form) 📜

Hii hapa ndio official source code ya grammatical rules za JSON:

```text
json
    element

value
    object
    array
    string
    number
    "true"
    "false"
    "null"

object
    '{' ws '}'
    '{' members '}'

members
    member
    member ',' members

member
    ws string ws ':' element

array
    '[' ws ']'
    '[' elements ']'

elements
    element
    element ',' elements

element
    ws value ws

string
    '"' characters '"'

characters
    ""
    character characters

character
    '0020' . '10FFFF' - '"' - '\'
    '\' escape

escape
    '"'
    '\'
    '/'
    'b'
    'f'
    'n'
    'r'
    't'
    'u' hex hex hex hex

hex
    digit
    'A' . 'F'
    'a' . 'f'

number
    integer fraction exponent

integer
    digit
    onenine digits
    '-' digit
    '-' onenine digits

digits
    digit
    digit digits

digit
    '0'
    onenine

onenine
    '1' . '9'

fraction
    ""
    '.' digits

exponent
    ""
    'E' sign digits
    'e' sign digits

sign
    ""
    '+'
    '-'

ws
    ""
    '0020' ws
    '000A' ws
    '000D' ws
    '0009' ws
```

---

## 4. Main Examples za JSON 🇰🇪

Hii hapa ni mfano wa file kamili ya JSON inayotumia data types zote:

```json
{
  "developer": "Maxwell Nganga",
  "country": "Kenya",
  "mtaa": "Nairobi",
  "isEmployed": true,
  "experienceYears": 3,
  "skills": ["JavaScript", "Python", "React", "APIs"],
  "projects": [
    {
      "title": "Kenyan JS Documentation",
      "license": "MIT",
      "isPublic": true,
      "stars": 150
    }
  ],
  "preferences": {
    "theme": "dark",
    "editor": "VS Code",
    "coffeeCupsPerDay": 2
  },
  "spouse": null
}
```

---

## 📜 Credits & License
* Imejengwa kulingana na standard ya [json.org](https://www.json.org/) iliyoasisiwa na Douglas Crockford na kiwango cha kimataifa cha **ECMA-404**.
* Imetolewa chini ya leseni ya **MIT License**.
