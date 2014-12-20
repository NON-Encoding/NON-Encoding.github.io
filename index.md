---
layout: default
title:  "NON-Encoding"
---

# *N*ull *O*r *N*ext-*E*ncoding

**NONE** is a variable-length universal character encoding and code-page standard.

It is the intent of the encoding to become the only encoding needed and used;\\
to make both programming and working with texts less frustrating.

Encoding finally has to become a **non-e**ncoding.

## Encoding-Scheme

**NONE** encoding is lightening simple and regular.

1. Each character is identified by a single code, its character-code.
2. Any character-code is encoded as a sequence of one or more bytes.
3. If the MSB of a byte is `1` the character-code continues.
4. If the MSB of a byte is `0` it is the last byte of a character-code.
5. The bits and bytes are in Big-Endian order.

Thereby the different character-codes can be encoded with one or more bytes:

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
	<td>&nbsp;2<sup>7</sup> = 128</td>
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
* <code>2<sup>14</sup> = 16,384</code> possible 2-byte characters (that is 8 times more than `UTF-8`)
* any sequence of bits and bytes has a meaning (except for last byte of an input)
* the schema naturally extends to any amount of bytes for a character
* a start or end byte of a character can be identified simple and efficient 
  within any stream of bytes without special knowledge (e.g. about the code-page).

## Code-Page

**NONE** _encoding_ and _decoding_ from and to character-codes is as 
straightforward as it can get. All character-codes are allocated on the 
code page in such a way that the _encoded_ sequence of bits of a character's 
bytes interpreted as one unsigned integer is the character code (code point).

<table class='encoding'>
<tr>
	<th></th>
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
<i class='ascii'></i><u class='byte1'></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u>
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
&nbsp;
</div>
The above table shows the distribution of usable (white <i class='region'> </i>)
and unusable (cream <u class='region'> </u>) regions within the first 2 bytes each having
a code space of 128 characters. 
The first region is assigned to the `ASCII` <i class='region ascii'></i> 
character set.

This comb like pattern reoccurs 128 times within the 3-byte range in the
second half of its code space. This again reoccurs 128 times within for 
4-byte range and so forth. 
The `ASCII` region though is an artefact of single byte characters and special 
to the first comb. It does not reoccur in later combs.

<!--
TODO byte 1,2,3,4
-->

The assignment of characters to codes is withal not arbitrary. 
With `ASCII` as basis any other character gets assigned to a code so that a 
handful of crucial properties emerge that make arithmetic of common text 
processing tasks simpler and more efficient.



## Properties

<!-- 
### Arithmetic's

<table class='big'>
<tr><th></th><th>+</th><th>=</th></tr>
<tr><td>e</td><td>´</td><td>é</td></tr>
<tr><td>a</td><td>´</td><td>á</td></tr>
<tr><td>e</td><td>^</td><td>ê</td></tr>
<tr><td>a</td><td>^</td><td>â</td></tr>
</table>
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
Considering that makes the unpleasant cascades of conditional constructs needed 
to encode or decode `UTF-8` almost appear like a triviality. 

Regrettably `Unicode` is not **one** text encoding, it does not end encoding 
incompatibilities and constant recoding but rather gives birth to complex code 
trapped in a dilemma to choose between efficient or correct.

#### The Future

It's _text_, we all know how to handle that.




