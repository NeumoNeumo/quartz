---
tags:
  - coding
  - encoding
  - CS
  - history
---
# Basic concepts

## Unicode 

Universal Coded Character Set, a.k.a. UCS or **Unicode**, defines the the map
from a character to single or multiple *code points*, the numerical values in
the Unicode *codespace*. Situations of the map:
- Some code points are not assigned;
- Some characters can be encoded into different code points;
- Some characters like ю́ are encoded as a combination of multiple code points.

These make it impossible to [[UTF#Counting|count characters]] in constant time. ^counting

## UTF & USC

Storage of code points has multiple Unicode Transformation Formats (**UTF**),
including UTF-8, UTF-16 and UTF-32 with 8-bit, 16-bit and 32-bit *code units*
respectively. Therefore, the same character probably needs 4 code units, 2 code
units or 1 code unit to store in UTF-8, UTF-16 and UTF-32 respectively.
^code-units

From a historical view, Joseph D. Becker initially assumed 16 bits per character
would suffice as shown in the [first Unicode draft proposal](http://unicode.org/history/unicode88.pdf). So 16-bit fixed-width UCS-2 is proposed. However, with CJK characters added, the code point had to expand to 32 bits, leading to UTF-16, the variable-width encoding that arose from UCS-2 which is obsoleted today. We could also use a single 32-bit code unit to represent the 32-bit code point. That is UTF-32 a.k.a UCS-4.

# Common sense

1. In both UTF-8 and UTF-16 encodings, a code point may take up to 4 bytes.
2. `widechar` is 2 bytes in size on some platforms, 4 on others.
3. UTF-8 and UTF-32 yield the same order when sorted lexicographically. UTF-16
does not.
4. Unicode 码位的汉字排序是康熙字典序，而不是新华字典序。`Unihan` 数据库可用于实现拼音排序

# Prefer to use UTF-8

reference: https://utf8everywhere.org/

## Storage

Asian characters take more in UTF-8 than UTF-16. However, because the dominance
of network text interfaces, including XML, HTTP, CSS, are all in English
letters, UTF-8 exhibits higher overall space occupation for its efficient encoding for English.

|                 | HTML Source (Δ UTF-8) | Dense text (Δ UTF-8) |
| ---------------:|:---------------------:|:--------------------:|
|           UTF-8 |      767 KB (0%)      |     222 KB (0%)      |
|          UTF-16 |    1 186 KB (+55%)    |    176 KB (−21%)     |
|    UTF-8 zipped |     179 KB (−77%)     |     83 KB (−63%)     |
| UTF-16LE zipped |     192 KB (−75%)     |     76 KB (−66%)     |
| UTF-16BE zipped |     194 KB (−75%)     |     77 KB (−65%)     |
(Japan article, retrieved from the Japanese Wikipedia on 2012–01–01)

Therefore, UTF-16 only surpasses UTF-8 in encoding density on dense texts.

##  Endianess

Longer [[#^code-units|code units]] necessitate the consideration of endianess in
UTF-16 and UTF-32 while UTF-8 does not have the issue.

## Counting

A common misconception about UTF-16 is assuming it as an fix-width encoding so
that counting costs only constant time. However, UTF-16 has a variable width. (But UTF-16 arose from an earlier obsolete fixed-width 16-bit encoding, now known as UCS-2)
Additionally even a fixed width encoding like UTF-32 cannot guarantee the
correctness of counting in constant time since multiple code points can
represent one perceived character as [[#^counting|mentioned before]].

# Messy Code

# 乱码类型对照表

| 名称  | 示例                                | 特点               | 产生原因                     |
| --- | --------------------------------- | ---------------- | ------------------------ |
| 古文码 | 鑿辨溪瑕恬ソ濂藉口涔豺お澶十惺涓?                 | 大都为不认识的古文，并加杂日韩文 | 以GBK方式读取UTF-8编码的中文       |
| 口字码 | □□□□□□□□                          | 大部分字符为小方块        | 以UTF-8的方式读取GBK编码的中文      |
| 符号码 | ς ±æ è! å¥1⁄2å¥1⁄2 å¡ä¹ å¤©å¤©å ä | 大部分字符为各种符号       | 以ISO8859-1方式读取UTF-8编码的中文 |
| 拼音码 | ÓÉÔÂÔaoÃoÃoÃÑgǐoììììòÉ ǐ          | 头顶带有各种类似声调符号的字母  | 以ISO8859-1方式读取GBK编码的中文   |
| 问句码 | 由月要好好学习天天向??                      | 奇数长度时最后字符变问号     | UTF-8->GBK->UTF-8        |
| 锟拷码 | 锟斤拷锟斤拷要锟矫猴拷学习锟斤拷...               | 全中文且大量重复"锟斤拷"    | GBK->UTF-8→GBK           |

## 锟斤拷 

Summarized from [this answer](https://www.zhihu.com/question/23024782/answer/36719691).

1. Two successive rare characters that cannot display correctly in some software.
2. The software replace it to two �� (`U+FFFD`), which is 
``` text
0xEF 0xBF 0xBD   0xEF 0xBF 0xBD
```
in UTF-8.
3. The text is directly copy and paste elsewhere and decoded as GBK.
Then we have
``` text
锟（0xEFBF）
斤（0xBDEF）
拷（0xBFBD）
```

锟斤拷生成器: https://blog.sww.moe/tools/kunjinkao/
乱码恢复: http://www.mytju.com/classCode/tools/messyCodeRecover.asp