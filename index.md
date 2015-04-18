---
layout: default
title:  "non-encoding"
---

<table id="title"><tr><td>
<h1><em>N</em>ull<br/><em>O</em>r<br/><em>N</em>ext<br/><em>E</em>ncoding</h1>
</td>
<td width="40%" style="text-align: justify;">
<b>none</b> is a universal variable-length character encoding <br/> 
and code-page standard.<br/>
<br/>
The goal is that <b>none</b> becomes the only <b>text</b> encoding needed and used;<br/>
to make both programming and working with texts less frustrating.<br/>
<br/>
Text encoding finally has to become a <b>none</b> question.
</td></tr></table>

## Encoding-Scheme

**none** encoding is lightening simple and regular.

1. Each character is identified by a single code, its character-code.
2. Any character-code is encoded as a sequence of one or more bytes.
3. If the MSB of a byte is `1` the character-code continues.
4. If the MSB of a byte is `0` it is the last byte of a character-code.
5. The bits and bytes are in Big-Endian order.

The different character-codes can be encoded with one or more bytes:

<table class='encoding'>
<tr>
	<th>Byte 1</th>
	<th>Byte 2</th>
	<th>Byte 3</th>
	<th>Byte 4</th>
	<th>Code Space</th>
</tr>
<tr>
	<td class='byte last'>0xxxxxxx</td>
	<td></td>
	<td></td>
	<td></td>
	<td>&nbsp;2<sup>7&nbsp;</sup> = 128</td>
</tr>
<tr>
	<td class='byte'>1xxxxxxx</td>
	<td class='byte last'>0xxxxxxx</td>
	<td></td>
	<td></td>
	<td>&nbsp;2<sup>14</sup> = 16,384</td>
</tr>
<tr>
	<td class='byte'>1xxxxxxx</td>
	<td class='byte'>1xxxxxxx</td>
	<td class='byte last'>0xxxxxxx</td>
	<td></td>
	<td>&nbsp;2<sup>21</sup> = 2,097,152</td>
</tr>
<tr>
	<td class='byte'>1xxxxxxx</td>
	<td class='byte'>1xxxxxxx</td>
	<td class='byte'>1xxxxxxx</td>
	<td class='byte last'>0xxxxxxx</td>
	<td>&nbsp;2<sup>28</sup> = 268,435,456</td>
</tr>
<tr>
	<th colspan="4">...</th>
	<td></td>
</tr>
</table>

The qualities of this encoding scheme are:

* `ASCII` compatible (single byte with `0` MSB)
* <code>2<sup>14</sup> = 16,384</code> possible 2-byte characters (that is 8 times `UTF-8`)
* any complete sequence of bytes translates to valid codes
* the schema naturally extends to any amount of bytes for a character
* all non-logographic scripts could be encoded by a maximum of 2 bytes!
* start or end bytes of a character can be identified simple and efficient 
  within streams of bytes without context knowledge

## Code-Page

**none** _encoding_ and _decoding_ from and to character-codes is as 
straightforward as it can get. All character-codes are allocated on the 
code page in such a way that the _encoded_ sequence of bits of a character's 
bytes interpreted as one unsigned integer is the character code (code point).

<table class='encoding'>
<tr>
	<th><i>Example:</i></th>
	<th></th>
	<th></th>
	<th>Byte 1</th>
	<th>Byte 2</th>
	<th>Code</th>
</tr>
<tr>
	<th>Bytes</th>
	<td></td>
	<td></td>
	<td class='byte'>11100000</td>
	<td class='byte'>01100101</td>
	<td></td>
</tr>
<tr>
	<th>uint32&nbsp;</th>
	<td>00000000</td>
	<td>00000000</td>
	<td class='charcode'>11100000</td>
	<td class='charcode'>01100101</td>
	<td>= 57445</td>
</tr>
</table>

The code for a 2-byte character is e.g. extracted from the character's bytes 
to a  32-bit integer by loading them into a register - vice versa a code could 
be split into _encoded_ bytes by simply removing leading zero bytes. 

All codes (numeric values) that cannot be used in such a way aren't allocated. 

<div class='page'>
<i class='ascii'>A</i><u class='byte1'></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u>
<u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u>
<u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u>
<u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u>
<u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u>
<u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u>
<u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u>
<u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u>
<i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u>
<i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u>
<i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u>
<i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u>
<i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u>
<i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u>
<i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u>
<i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u><i></i><u></u>
</div>
<br/>

The above table shows the distribution of usable (<i class='region'> </i>)
and unusable (<u class='region'> </u>) regions within the first 2 bytes each having
a code space of 128 characters. 
The first region is assigned to the `ASCII` <i class='region ascii'>A</i> 
character set.

This comb like pattern reoccurs 128 times within the 3-byte range in the
second half of its code space. This again reoccurs 128 times within for 
4-byte range and so forth. 
The `ASCII` region though is an artefact of single byte characters and special 
to the first comb. It does not reoccur in later combs.

In addition no codes with a `1000 0000` byte are assigned. These are 
reserved for an alternative fixed length encoding only used in memory.


## Properties
The assignment of characters to codes is withal not arbitrary. 
With `ASCII` as basis any other character gets assigned to a code so that a 
handful of crucial properties emerge that make arithmetic of common text 
processing tasks simpler and more efficient.

**Definiteness:** There is one and only one sequence of bytes to represent a 
particular character. Characters do encode meaning, never presentation aspects:
_1 character **=** 1 code **=** 1 sequence of bytes_.
 
**Analogousness:** If two sequences of bytes are equal they always do represent 
the same sequence of characters: 
_bytes of a sequence of characters **=** sequence of bytes of those characters_.

**Reducibility:** Reduction to Roman/ASCII is done by dropping all but a 
character's last byte. This implies that characters that are not based on Roman 
letters or digits never have a final byte that would indicate such a relation.

**Composability:** composition of letters and diacritics is done by adding 
bytes or codes. It follows that characters that are not independent 
(and as such also not members of a alphabet) do use the `NUL` final byte.

<!-- 
**Alphabetical Arrangement:** position and distance between letters or digits 
within the same alphabet is calculated by adding and subtracting their codes.

Note: the alphabet is a feature of a language or writing system but encoding 
is about scripts. The same letter can have different positions in different
languages as the letter `ä` has in e.g. german and swedish.
-->

## Computations
Given the encoding-scheme, the code-page arrangement and the properties of
character assignment common text processing tasks have a low computational
complexity and are straight forward to implement.

Character...

- **decoding:** _O(1)_ (copy to register)
- **encoding:** _O(1)_ (drop leading zero bytes)
- **normalisation:** _0_ (not needed)

Character sequence (of length _n_; encoded as bytes)...

- **length:** _O(n)_ (count bytes with MSB of zero)
- **equals:** _O(n)_ (compare byte by byte or code by code for equality)
- **m-th character:** _O(min(n,m))_ (count bytes with zero MSB)
- **romanisation:** _O(n)_ (drop bytes with one MSB)
- **deaccentuate:** _O(n)_ (drop bytes with one MSB before ASCII letter)


## Extensions
Encoding is a balancing act between compact representation 
(what benefits from a variable-length encoding) and computational efficiency 
(what benefits from a fixed-length encoding).

While the encoding-scheme is a variable-length encoding made for compact 
representation it can be extended to different fixed length forms without 
contradicting the properties or introduce multiple distinct encodings. 

To extend the variable-length encoding to a fixed with of 2, 3 or 4 bytes per
character the characters encoded with less than the chosen length are filled 
will the reserved byte `1000 0000`. 

		variable                                  0110 0000
		fixed-2                        1000 0000  0110 0000
		fixed-3             1000 0000  1000 0000  0110 0000
		fixed-4  1000 0000  1000 0000  1000 0000  0110 0000
		
A fixed-length of less than 4 bytes means that characters encoded in 3 or 4 
bytes cannot be represented. This is useful anyhow as most scripts are 
represented in 1 or 2 bytes per character.

As the byte `1000 0000` does never occur as part of the actual code-point value
a extended form is easily recognisable and can be stripped away or added on the
borders of a system or program or module therein. 

<!--
The internal code page could always mask away the 1 MSBs

1000 0000  1000 0000  1000 0000  0110 0000
0111 1111  0111 1111  0111 1111  1111 1111
0000 0000  0000 0000  0000 0000  0110 0000

this way it does not matter if the value (as 32-bit integer) was extended or not.
-->

## Motivation

#### History
Encoding is a necessity to give bits and bytes the meaning of characters and 
text. 
Historically a variety of encodings have coexisted on different systems for 
different scripts. 
Each language space had its own predominant encoding that often also differed 
for the diverse systems. 

When text content started to cross system borders more frequently due to growing
interconnection of computer systems their users were faced with a new kind of
incompatibly as programs could not handle the bits and bytes of _alien_ text 
correctly.

Interconnected programs and systems that shared text also needed to share a
commonly understood encoding. But a universal encoding comes with 
new problems: Instead of one script it now had to encode characters of all the 
world's scripts and a wide variety of other symbols while still being efficient. 

#### The Unicode Dilemma
Today `Unicode` as `UTF-8` or `UTF-16` encoding is used for more and more
text documents. The idea of a universal encoding is widely established and very 
appreciated among programmers. 

The vision of a common _encoding_ and as a consequence thereof the 
_disappearance_ of encoding as a source of complexity and failure seems to be
within one's grasp. 

This is an illusion though. On closer inspection `Unicode` unfolds critical flaws. 
[Modifier characters](http://www.unicode.org/charts/#CombiningDiacriticalMarks) 
corrupt a equivalence between a code-point and a visible character whereby 
character count and indexed access is either incorrect or inefficient. 
[Normalisation forms](http://unicode.org/reports/tr15/) grotesquely exhibit
how the same character can be encoded differently; as a consequence a 
banal equality check is far from being trivial or efficient.
[Presentation forms](http://www.unicode.org/charts/PDF/UFB00.pdf),
[surrogate pairs](http://unicodebook.readthedocs.org/en/latest/unicode_encodings.html#utf-16-surrogate-pairs)
or [byte order marks](http://unicodebook.readthedocs.org/en/latest/unicode_encodings.html#byte-order-marks-bom)
are likewise unfortunate. 

Paradoxically `Unicode` includes *multiple* encodings so that programs still 
have to make their best effort to guess text encoding right - 
exactly what a *uni*versal encoding should have corrected. 
To make matters worse the popular `UTF-8` and `UTF-16` encoding schemata do not
render the occurrence of malformed byte sequences impossible. 
Constantly validating text IO, however, is unreasonable inefficient, 
wherefore it is often dropped, what in turn is incorrect.
Considering all that makes the unpleasant cascades of conditional constructs needed 
to encode or decode `UTF-8` almost appear like a triviality. 

Regrettably `Unicode` is not **one** text encoding, it does not end encoding 
incompatibilities and constant recoding but rather gives birth to complex code 
trapped in a dilemma to choose between efficient or correct.

#### The Future

It's _text_, we all know how to handle that.


## Contribution
It requires great effort and knowledge about the worlds scripts to arrange the
code-page in such a way that the properties described above arise. 
The project requires the help of language experts to take this step. 

From the numbers I know of it should be possible. 
Roughly there are about 200 scripts worldwide.
Most of them are not [logographic](http://en.wikipedia.org/wiki/Logogram).
I made a rough estimate of about 40 characters per script on average:

		200 x 40 = 8000

That is roughly halve of the code-space available using 2 bytes, what is the
goal for these scripts. Logographic scripts are encoded using 3 or 4 bytes. 
There is plenty of space available - the main question here is: What is a good
way to arrange them on the code-page so that typical text-processing tasks are
simple to implement. 

Maybe I missed something? Maybe you have ideas of more properties that are
important or could be added?

If you want to contribute in any way please [contact me](mailto:jaanbernitt+none@gmail.com)
or use the [project's issue system](https://github.com/NON-Encoding/NON-Encoding.github.io/issues).

