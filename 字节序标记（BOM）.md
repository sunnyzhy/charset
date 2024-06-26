# 字节序标记（BOM）

## 概念

在将逻辑形式的码元序列(或可称之为逻辑编码)映射为物理形式的字节序列(或可称之为物理编码)时，因系统平台的差异，存在一个字节序(Byte-Order字节顺序)的问题。

而字节序问题的存在，导致在某些场合下，需要对文本字符所采用的字节序予以明确说明。Unicode/UCS 规范中所推荐的用于说明字节序的方法是使用 BOM 字节序标记(Byte-Order Mark 字节顺序标记)。

字节序标记 BOM 采用的是 Unicode 码点值为 FEFF 的字符，因此 BOM 实际上可认为是该字符(U+FEFF)的别名。

最初，字符 U+FEFF 如果出现在字节流的开头，则用来标识该字节流的字节序——是高位在前还是低位在前；如果它出现在字节流的中间，则表达为该字符的原义——零宽度不中断空格(ZERO WIDTH NO-BREAK SPACE 零宽度无断空白)。

不过，从 Unicode 3.2 开始，U+FEFF 只能出现在字节流的开头，且只能用于标识字节序，除此以外的用法已被舍弃。取而代之的是使用 U+2060 来表示零宽度不中断空格。

## 大端序(Big Endian)与小端序(Little Endian)

UTF-8 编码，其本身并不存在字节序的问题，但仍然有可能用 BOM 来标示某文本是 UTF-8 编码，该 BOM 为字节流的前三个字节 ```0xEF 0xBB 0xBF```。

UTF-16 编码，如果字节序列为大端序，则该 BOM 为字节流的前两个字节 ```0xFE 0xFF```；如果字节序列为小端序，则该 BOM 为字节流的前两个字节 ```0xFF 0xFE```。

UTF-32 编码，如果字节序列为大端序，则该 BOM 为字节流的前四个字节 ```0x00 0x00 0xFE 0xFF```；如果字节序列为小端序，则 BOM 该为字节流的前四个字节 ```0xFF 0xFE 0x00 0x00```。

**在 UFT-8 编码格式的文本中，如果添加了BOM，则只用它来标示该文本是由 UTF-8 编码方式编码的，而不用来说明字节序，因为 UTF-8 编码根本就不存在字节序问题。**

|字节序标记（BOM）|十六进制|
|--|--|
|UTF-8|EF BB BF|
|UTF-16(Big Endian)|FE FF|
|UTF-16(Little Endian)|FF FE|
|UTF-32(Big Endian)|00 00 FE FF|
|UTF-32(Little Endian)|FF FE 00 00|
