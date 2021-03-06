<p align="center">
    <br/>
    <a href="https://github.com/ziishaned/learn-regex">
        <img src="https://i.imgur.com/bYwl7Vf.png" alt="Learn Regex">
    </a>
    <br /><br />
    <p>
        <a href="https://twitter.com/ziishaned">
            <img src="https://img.shields.io/twitter/follow/ziishaned.svg?style=social" />
        </a>
        <a href="https://github.com/ziishaned">
            <img src="https://img.shields.io/github/followers/ziishaned.svg?label=Follow%20%40ziishaned&style=social" />
        </a>
    </p>
</p>

## Translations:

* [English](README.md)
* [Español](translations/README-es.md)
* [Français](translations/README-fr.md)
* [Português do Brasil](translations/README-pt_BR.md)
* [中文版](translations/README-cn.md)
* [日本語](translations/README-ja.md)
* [한국어](translations/README-ko.md)
* [Turkish](translations/README-tr.md)
* [Greek](translations/README-gr.md)
* [Magyar](translations/README-hu.md)
* [Polish](translations/README-pl.md)
* [Русский](translations/README-ru.md)
* [Tiếng Việt](translations/README-vn.md)
* [فارسی](translations/README-fa.md)

## عبارت باقاعده چیست؟

> عبارت باقاعده گروهی از کاراکترها  یا نشانه ها  ست که برای پیدا کردن الگوی خاصی در یک متن استفاده می شود.

یک عبارت منظم الگویی است که با رشته‌ای از چپ به راست مطابقت دارد. عبارت باقاعده  رامی‌توان برای جایگزینی یک متن درون یک رشته یا برای اعتبارسنجی  فرم‌ها ونیز برای استخراج یک زیر رشته از یک رشته‌ی دیگر  براساس یک الگو و در موارد بی شمار دیگری استفاده کرد. بجای استفاده از کلمه‌ی "Regular experssion"  معمولا از شکل اختصاری آن به صورت "regex" یا "regexp" استفاده می‌شود.

فرض کنید برنامه‌ای نوشته‌اید و می‌خواهید قواعدی را برای انتخاب نام کاربری توسط کاربر ایجاد کنید. ما می خواهیم اجازه دهیم که نام کاربری شامل حروف، اعداد، زیر خط و خط ربط باشد. همچنین  می‌خواهیم تعداد کاراکترهای نام کاربری محدود باشد.
برای ارزیابی نام کاربری از عبارت باقاعده ی زیر استفاده می‌کنیم:

<br/><br/>
<p align="center">
  <img src="../img/regexp-fa.png" alt="Regular expression">
</p>

عبارت باقاعده ی بالا می تواند رشته هایی مانند `john-doe` ، `jo-hn_doe` و `john12_as` را بپذیرد. این عبارت باقاعده نمی تواند `Jo` را بپذیرد چون علاوه برآنکه دارای حروف بزرگ است، طول کمی نیز دارد.

## جدول محتوا

- [تطبیق گرهای ابتدایی](#1)
- [فرا کاراکترها](#2)
  - [نقطه](#21-full-stop)
  - [مجموعه کاراکترها](#22-character-set)
    - [مجموعه کاراکترهای منفی](#221-negated-character-set)
  - [تکرار ها](#23-repetitions)
    - [ستاره](#231-the-star)
    - [بعلاوه](#232-the-plus)
    - [علامت سوال](#233-the-question-mark)
  - [براکت ها](#24-braces)
  - [گروه کاراکتری](#25-character-group)
  - [جایگزین](#26-alternation)
  - [Escaping special character](#27-escaping-special-character)
  - [Anchors](#28-anchors)
    - [Caret](#281-caret)
    - [Dollar](#282-dollar)
- [Shorthand Character Sets](#3-shorthand-character-sets)
- [Lookaround](#4-lookaround)
  - [Positive Lookahead](#41-positive-lookahead)
  - [Negative Lookahead](#42-negative-lookahead)
  - [Positive Lookbehind](#43-positive-lookbehind)
  - [Negative Lookbehind](#44-negative-lookbehind)
- [Flags](#5-flags)
  - [Case Insensitive](#51-case-insensitive)
  - [Global search](#52-global-search)
  - [Multiline](#53-multiline)
- [Greedy vs lazy matching](#6-greedy-vs-lazy-matching)

<a name="1"></a>
## 1. تطبیق گرهای ابتدایی

عبارت باقاعده الگویی از کاراکترها برای انجام عمل جست‌وجو در متن است. برای مثال معنای عبارت باقاعده ی `the` به این صورت است که: ابتدا حرف `t` به دنبال آن حرف `h` و در نهایت حرف `e` انتخاب می شوند.

<pre>
"the" => The fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[امتحان کنید](https://regex101.com/r/dmRygT/1)

عبارت باقاعده‌ی `123` با رشته‌ی `123` مطابقت می‌کند. عبارت باقاعده به این صورت عمل می کند که هر کاراکتری در عبارت باقاعده با هر کاراکتر از رشته ورودی مطابقت داده می شود. عبارات باقاعده درحالت عادی به بزرگی و کوچکی حروف حساس هستند بنابراین عبارت باقاعده ی `The` رشته‌ی ‍`the` را پوشش نمی‌دهد.

<pre>
"The" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[امتحان کنید](https://regex101.com/r/1paXsy/1)
<a name="2"></a>

## 2. فرا کاراکترها

فرا کاراکترها بلاک‌هایی از عبارات باقاعده هستند. فرا کاراکترها به جای مفهوم پیش‌فرض خود، به صورت خاصی تفسیر می‌شوند. برخی از فرا کاراکترها معنای خاصی دارند و در درون براکت‌ها نوشته می‌شوند. فرا کاراکترهای به صورت ذیل‌اند:

|فراکاراکتر|شرح|
|:----:|----|
|.|نقطه هر کاراکتر تنها به جز کاراکتر line break را مچ می‌کند.|
|[ ]|کاراکتر کلاس. هر کاراکتر درون براکت‌ها مچ می‌شود.|
|[^ ]|کاراکتر کلاس معکوس. هر کاراکتری که درون براکت‌ها نباشد، مچ می‌شود.|
|*|صفر یا هر چند تکرار از سمبل قبلی را مچ می‌کند.|
|+|یک یا چند تکرار از سمبل قبلی را مچ می‌کند.|
|?|Makes the preceding symbol optional.|
|{n,m}|به تعداد n تا m کاراکتر را مچ می‌کند.|
|(xyz)|گروه کاراکترها. کاراکترهای xyz را به همین ترتیب مچ می‌کند.|
|&#124;|Alternation. Matches either the characters before or the characters after the symbol.|
|&#92;|کاراکتر بعدی را اسکیپ می‌کند. مچ شدن کاراکترهای رزروی مانند را امکان پذیر می‌کند. <code>[ ] ( ) { } . * + ? ^ $ \ &#124;</code>| 
|^| شروع ورودی را مچ می‌کند.|
|$|پایان ورودی را مچ می‌کند.|

## 2.1 فول استاپ
فول استاپ `.` ساده‌ترین مثال از فراکاراکتر‌هاست. این فراکاراکتر هر کاراکتر تنها به استثنای کاراکتر‌های سرخط و خط بعدی را مچ می‌کند. برای مثال عبارت باقاعده‌ی `.ar` به معنای مچ شدن هر کاراکتری به دنبال آن حرف `a` و سپس حرف `r` است.

<pre>
".ar" => The <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[امتحان کنید](https://regex101.com/r/xc9GkU/1)

## 2.2 مجموعه کاراکترها

مجموعه کاراکتر‌ها، کلاس کاراکترها نیز خوانده می‌شوند. از کروشه برای مشخص کردن مجموعه کاراکترها استفاده می‌شود. برای مشخص کردن محدوده کاراکترها از خط فاصله استفاده می‌شود. ترتیب کاراکترها در درون کروشه مهم نیست. مثلاً عبارت باقاعده `[Tt]he` به معنای مچ شدن یک `T` به دنبال آن یک `t` و در نهایت حروف `h`و `e` است.

<pre>
"[Tt]he" => <a href="#learn-regex"><strong>The</strong></a> car parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[امتحان کنید](https://regex101.com/r/2ITLQ4/1)

یک نقطه درون مجموعه کاراکترها به معنای یک نقطه معمولی است. در واقع نقطه اسکیپ می‌شود. مثلاً برای عبارت باقاعده‌ی `ar[.]` مچ به صورت زیر خواهد بود.

<pre>
"ar[.]" => A garage is a good place to park a c<a href="#learn-regex"><strong>ar.</strong></a>
</pre>

[امتحان کنید](https://regex101.com/r/wL3xtE/1)

### 2.2.1 مجموعه کاراکتری قرینه

درحالت کلی کاراکتر هت نمایانگر شروع رشته است. اما وقتی که در آغاز مجموعه کاراکترها در درون کرشه استفاده شود، عبارت باقاعده را قرینه می‌کند. برای مثال عبارت باقاعده‌ی [^c]ar به معنای مچ شدن هر کاراکتری به جز `c` و به دنبال ‌آن کاراکتر‌های `a`  , `r` است.

<pre>
"[^c]ar" => The car <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[امتحان کنید](https://regex101.com/r/nNNlq3/1)

## 2.3 تکرارها

فراکاراکترهای `+`و `*`و `?` برای مشخص کردن تعداد دفعات مچ شدن زیر الگوها استفاده می‌شوند. این فراکاراکترها در موقعیت‌ها مختلف، معانی مختلفی دارند.


### 2.3.1 ستاره

کاراکتر `*` صفر یا چند تکرار از کارکتر پیشین را مچ می‌کند. عبارت باقاعده‌ی `a*` به معنای تکرار صفر یا چند مورد کاراکتر `a` است. اما اگر به مجموعه کاراکترها اعمال شود به معنای تکرار تمام عناصر آن مجموعه کاراکتری است. مثلاً عبارت باقاعده‌ی `[a-z]*` به معنای هر تعداد حروف کوچک در یک سطر است.

<pre>
"[a-z]*" => T<a href="#learn-regex"><strong>he</strong></a> <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>parked</strong></a> <a href="#learn-regex"><strong>in</strong></a> <a href="#learn-regex"><strong>the</strong></a> <a href="#learn-regex"><strong>garage</strong></a> #21.
</pre>

[امتحان کنید](https://regex101.com/r/7m8me5/1)

سمبل `*` به همراه کاراکتر `.` برای مچ شدن هر رشته‌ای از کاراکترها استفاده میشود`.*`. سمبل `*` به همراه کاراکتر whitespace `\s` به منظور مچ شدن رشته‌ای از کاراکترهای whitespace استفاده می‌شود. مثلاً در عبارت باقاعده‌ی `\s*cat\s*` صفر یا چند فضای خالی مچ می‌شود به دنبال آن کاراکتر `c` و بعد کاراکتر `a` و  کاراکتر `t` و درنهایت صفر یا چند فضای خالی مچ خواهند شد.

<pre>
"\s*cat\s*" => The fat<a href="#learn-regex"><strong> cat </strong></a>sat on the con<a href="#learn-regex"><strong>cat</strong></a>enation.
</pre>

[امتحان کنید](https://regex101.com/r/gGrwuz/1)

### 2.3.2 جمع

کاراکتر `+` یک یا چند تکرار از کاراکتر‌های پیشین را مچ می‌کند. برای مثال عبارت باقاعده‌ی `c.+t` به معنای مچ شدن یک کاراکتر `c` به دنبال آن حداقل یک کاراکتر دیگر و درنهایت کاراکتر `t` خواهد بود.

<pre>
"c.+t" => The fat <a href="#learn-regex"><strong>cat sat on the mat</strong></a>.
</pre>

[امتحان کنید](https://regex101.com/r/Dzf9Aa/1)

### 2.3.3 علامت سوال

در عبارات باقاعده‌، فراکاراکتر `?` کاراکتر پیشین را اختیاری می‌کند بدین معنی که صفر یا یک کاراکتر را مچ می‌کند. مثلاً عبارت باقاعده‌ی `[T]?he` به معنای مچ شدن صفر یا یک کاراکتر `T` و به دنبال آن کاراکتر های `h` و ‍`e` خواهد بود.

<pre>
"[T]he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

[امتخان کنید](https://regex101.com/r/cIg9zm/1)

<pre>
"[T]?he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in t<a href="#learn-regex"><strong>he</strong></a> garage.
</pre>

[امتحان کنید](https://regex101.com/r/kPpO2x/1)

## 2.4 Braces

In regular expression braces that are also called quantifiers are used to
specify the number of times that a character or a group of characters can be
repeated. For example, the regular expression `[0-9]{2,3}` means: Match at least
2 digits but not more than 3 ( characters in the range of 0 to 9).

<pre>
"[0-9]{2,3}" => The number was 9.<a href="#learn-regex"><strong>999</strong></a>7 but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[Test the regular expression](https://regex101.com/r/juM86s/1)

We can leave out the second number. For example, the regular expression
`[0-9]{2,}` means: Match 2 or more digits. If we also remove the comma the
regular expression `[0-9]{3}` means: Match exactly 3 digits.

<pre>
"[0-9]{2,}" => The number was 9.<a href="#learn-regex"><strong>9997</strong></a> but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[Test the regular expression](https://regex101.com/r/Gdy4w5/1)

<pre>
"[0-9]{3}" => The number was 9.<a href="#learn-regex"><strong>999</strong></a>7 but we rounded it off to 10.0.
</pre>

[Test the regular expression](https://regex101.com/r/Sivu30/1)

## 2.5 Capturing Group

A capturing group is a group of sub-patterns that is written inside Parentheses 
`(...)`. Like as we discussed before that in regular expression if we put a quantifier 
after a character then it will repeat the preceding character. But if we put quantifier
after a capturing group then it repeats the whole capturing group. For example,
the regular expression `(ab)*` matches zero or more repetitions of the character
"ab". We can also use the alternation `|` meta character inside capturing group.
For example, the regular expression `(c|g|p)ar` means: lowercase character `c`,
`g` or `p`, followed by character `a`, followed by character `r`.

<pre>
"(c|g|p)ar" => The <a href="#learn-regex"><strong>car</strong></a> is <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Test the regular expression](https://regex101.com/r/tUxrBG/1)

Note that capturing groups do not only match but also capture the characters for use in 
the parent language. The parent language could be python or javascript or virtually any
language that implements regular expressions in a function definition.

### 2.5.1 Non-capturing group

A non-capturing group is a capturing group that only matches the characters, but 
does not capture the group. A non-capturing group is denoted by a `?` followed by a `:` 
within parenthesis `(...)`. For example, the regular expression `(?:c|g|p)ar` is similar to 
`(c|g|p)ar` in that it matches the same characters but will not create a capture group.

<pre>
"(?:c|g|p)ar" => The <a href="#learn-regex"><strong>car</strong></a> is <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Test the regular expression](https://regex101.com/r/Rm7Me8/1)

Non-capturing groups can come in handy when used in find-and-replace functionality or 
when mixed with capturing groups to keep the overview when producing any other kind of output. 
See also [4. Lookaround](#4-lookaround).

## 2.6 Alternation

In a regular expression, the vertical bar `|` is used to define alternation.
Alternation is like an OR statement between multiple expressions. Now, you may be
thinking that character set and alternation works the same way. But the big
difference between character set and alternation is that character set works on
character level but alternation works on expression level. For example, the
regular expression `(T|t)he|car` means: either (uppercase character `T` or lowercase
`t`, followed by lowercase character `h`, followed by lowercase character `e`) OR
(lowercase character `c`, followed by lowercase character `a`, followed by
lowercase character `r`). Note that I put the parentheses for clarity, to show that either expression
in parentheses can be met and it will match.

<pre>
"(T|t)he|car" => <a href="#learn-regex"><strong>The</strong></a> <a href="#learn-regex"><strong>car</strong></a> is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[Test the regular expression](https://regex101.com/r/fBXyX0/1)

## 2.7 Escaping special character

Backslash `\` is used in regular expression to escape the next character. This
allows us to specify a symbol as a matching character including reserved
characters `{ } [ ] / \ + * . $ ^ | ?`. To use a special character as a matching
character prepend `\` before it.

For example, the regular expression `.` is used to match any character except
newline. Now to match `.` in an input string the regular expression
`(f|c|m)at\.?` means: lowercase letter `f`, `c` or `m`, followed by lowercase
character `a`, followed by lowercase letter `t`, followed by optional `.`
character.

<pre>
"(f|c|m)at\.?" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> sat on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/DOc5Nu/1)

## 2.8 Anchors

In regular expressions, we use anchors to check if the matching symbol is the
starting symbol or ending symbol of the input string. Anchors are of two types:
First type is Caret `^` that check if the matching character is the start
character of the input and the second type is Dollar `$` that checks if matching
character is the last character of the input string.

### 2.8.1 Caret

Caret `^` symbol is used to check if matching character is the first character
of the input string. If we apply the following regular expression `^a` (if a is
the starting symbol) to input string `abc` it matches `a`. But if we apply
regular expression `^b` on above input string it does not match anything.
Because in input string `abc` "b" is not the starting symbol. Let's take a look
at another regular expression `^(T|t)he` which means: uppercase character `T` or
lowercase character `t` is the start symbol of the input string, followed by
lowercase character `h`, followed by lowercase character `e`.

<pre>
"(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[Test the regular expression](https://regex101.com/r/5ljjgB/1)

<pre>
"^(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

[Test the regular expression](https://regex101.com/r/jXrKne/1)

### 2.8.2 Dollar

Dollar `$` symbol is used to check if matching character is the last character
of the input string. For example, regular expression `(at\.)$` means: a
lowercase character `a`, followed by lowercase character `t`, followed by a `.`
character and the matcher must be end of the string.

<pre>
"(at\.)" => The fat c<a href="#learn-regex"><strong>at.</strong></a> s<a href="#learn-regex"><strong>at.</strong></a> on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/y4Au4D/1)

<pre>
"(at\.)$" => The fat cat. sat. on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/t0AkOd/1)

##  3. Shorthand Character Sets

Regular expression provides shorthands for the commonly used character sets,
which offer convenient shorthands for commonly used regular expressions. The
shorthand character sets are as follows:

|Shorthand|Description|
|:----:|----|
|.|Any character except new line|
|\w|Matches alphanumeric characters: `[a-zA-Z0-9_]`|
|\W|Matches non-alphanumeric characters: `[^\w]`|
|\d|Matches digit: `[0-9]`|
|\D|Matches non-digit: `[^\d]`|
|\s|Matches whitespace character: `[\t\n\f\r\p{Z}]`|
|\S|Matches non-whitespace character: `[^\s]`|

## 4. Lookaround

Lookbehind and lookahead (also called lookaround) are specific types of
***non-capturing groups*** (Used to match the pattern but not included in matching
list). Lookarounds are used when we have the condition that this pattern is
preceded or followed by another certain pattern. For example, we want to get all
numbers that are preceded by `$` character from the following input string
`$4.44 and $10.88`. We will use following regular expression `(?<=\$)[0-9\.]*`
which means: get all the numbers which contain `.` character and  are preceded
by `$` character. Following are the lookarounds that are used in regular
expressions:

|Symbol|Description|
|:----:|----|
|?=|Positive Lookahead|
|?!|Negative Lookahead|
|?<=|Positive Lookbehind|
|?<!|Negative Lookbehind|

### 4.1 Positive Lookahead

The positive lookahead asserts that the first part of the expression must be
followed by the lookahead expression. The returned match only contains the text
that is matched by the first part of the expression. To define a positive
lookahead, parentheses are used. Within those parentheses, a question mark with
equal sign is used like this: `(?=...)`. Lookahead expression is written after
the equal sign inside parentheses. For example, the regular expression
`(T|t)he(?=\sfat)` means: optionally match lowercase letter `t` or uppercase
letter `T`, followed by letter `h`, followed by letter `e`. In parentheses we
define positive lookahead which tells regular expression engine to match `The`
or `the` which are followed by the word `fat`.

<pre>
"(T|t)he(?=\sfat)" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[Test the regular expression](https://regex101.com/r/IDDARt/1)

### 4.2 Negative Lookahead

Negative lookahead is used when we need to get all matches from input string
that are not followed by a pattern. Negative lookahead is defined same as we define
positive lookahead but the only difference is instead of equal `=` character we
use negation `!` character i.e. `(?!...)`. Let's take a look at the following
regular expression `(T|t)he(?!\sfat)` which means: get all `The` or `the` words
from input string that are not followed by the word `fat` precedes by a space
character.

<pre>
"(T|t)he(?!\sfat)" => The fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[Test the regular expression](https://regex101.com/r/V32Npg/1)

### 4.3 Positive Lookbehind

Positive lookbehind is used to get all the matches that are preceded by a
specific pattern. Positive lookbehind is denoted by `(?<=...)`. For example, the
regular expression `(?<=(T|t)he\s)(fat|mat)` means: get all `fat` or `mat` words
from input string that are after the word `The` or `the`.

<pre>
"(?<=(T|t)he\s)(fat|mat)" => The <a href="#learn-regex"><strong>fat</strong></a> cat sat on the <a href="#learn-regex"><strong>mat</strong></a>.
</pre>

[Test the regular expression](https://regex101.com/r/avH165/1)

### 4.4 Negative Lookbehind

Negative lookbehind is used to get all the matches that are not preceded by a
specific pattern. Negative lookbehind is denoted by `(?<!...)`. For example, the
regular expression `(?<!(T|t)he\s)(cat)` means: get all `cat` words from input
string that are not after the word `The` or `the`.

<pre>
"(?&lt;!(T|t)he\s)(cat)" => The cat sat on <a href="#learn-regex"><strong>cat</strong></a>.
</pre>

[Test the regular expression](https://regex101.com/r/8Efx5G/1)

## 5. Flags

Flags are also called modifiers because they modify the output of a regular
expression. These flags can be used in any order or combination, and are an
integral part of the RegExp.

|Flag|Description|
|:----:|----|
|i|Case insensitive: Sets matching to be case-insensitive.|
|g|Global Search: Search for a pattern throughout the input string.|
|m|Multiline: Anchor meta character works on each line.|

### 5.1 Case Insensitive

The `i` modifier is used to perform case-insensitive matching. For example, the
regular expression `/The/gi` means: uppercase letter `T`, followed by lowercase
character `h`, followed by character `e`. And at the end of regular expression
the `i` flag tells the regular expression engine to ignore the case. As you can
see we also provided `g` flag because we want to search for the pattern in the
whole input string.

<pre>
"The" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[Test the regular expression](https://regex101.com/r/dpQyf9/1)

<pre>
"/The/gi" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[Test the regular expression](https://regex101.com/r/ahfiuh/1)

### 5.2 Global search

The `g` modifier is used to perform a global match (find all matches rather than
stopping after the first match). For example, the regular expression`/.(at)/g`
means: any character except new line, followed by lowercase character `a`,
followed by lowercase character `t`. Because we provided `g` flag at the end of
the regular expression now it will find all matches in the input string, not just the first one (which is the default behavior).

<pre>
"/.(at)/" => The <a href="#learn-regex"><strong>fat</strong></a> cat sat on the mat.
</pre>

[Test the regular expression](https://regex101.com/r/jnk6gM/1)

<pre>
"/.(at)/g" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> <a href="#learn-regex"><strong>sat</strong></a> on the <a href="#learn-regex"><strong>mat</strong></a>.
</pre>

[Test the regular expression](https://regex101.com/r/dO1nef/1)

### 5.3 Multiline

The `m` modifier is used to perform a multi-line match. As we discussed earlier
anchors `(^, $)` are used to check if pattern is the beginning of the input or
end of the input string. But if we want that anchors works on each line we use
`m` flag. For example, the regular expression `/at(.)?$/gm` means: lowercase
character `a`, followed by lowercase character `t`, optionally anything except
new line. And because of `m` flag now regular expression engine matches pattern
at the end of each line in a string.

<pre>
"/.at(.)?$/" => The fat
                cat sat
                on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/hoGMkP/1)

<pre>
"/.at(.)?$/gm" => The <a href="#learn-regex"><strong>fat</strong></a>
                  cat <a href="#learn-regex"><strong>sat</strong></a>
                  on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/E88WE2/1)

## 6. Greedy vs lazy matching
By default regex will do greedy matching , means it will match as long as
possible. we can use `?` to match in lazy way means as short as possible

<pre>
"/(.*at)/" => <a href="#learn-regex"><strong>The fat cat sat on the mat</strong></a>. </pre>


[Test the regular expression](https://regex101.com/r/AyAdgJ/1)

<pre>
"/(.*?at)/" => <a href="#learn-regex"><strong>The fat</strong></a> cat sat on the mat. </pre>


[Test the regular expression](https://regex101.com/r/AyAdgJ/2)


## Contribution

* Open pull request with improvements
* Discuss ideas in issues
* Spread the word
* Reach out with any feedback [![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/ziishaned.svg?style=social&label=Follow%20%40ziishaned)](https://twitter.com/ziishaned)

## License

MIT &copy; [Zeeshan Ahmad](https://twitter.com/ziishaned)
