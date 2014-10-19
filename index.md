---
layout: default
title:  "NON-Encoding"
---

# *N*ull *O*r *N*ext*-E*ncoding

**NONE** is a variable-length character encoding and code-page standard.

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

<table class='encoding'>
<tr>
	<th>Byte 1</th>
	<th>Byte 2</th>
	<th>Byte 3</th>
	<th>Byte 4</th>
	<th>Code Space</th>
</tr>
<tr>
	<td class='byte'>0xxxxxxx</td>
	<td></td>
	<td></td>
	<td></td>
	<td>&nbsp;2<sup>7</sup> = 128</td>
</tr>
<tr>
	<td class='byte'>1xxxxxxx</td>
	<td class='byte'>0xxxxxxx</td>
	<td></td>
	<td></td>
	<td>&nbsp;2<sup>14</sup> = 16,384</td>
</tr>
<tr>
	<td class='byte'>1xxxxxxx</td>
	<td class='byte'>1xxxxxxx</td>
	<td class='byte'>0xxxxxxx</td>
	<td></td>
	<td>&nbsp;2<sup>21</sup> = 2,097,152</td>
</tr>
<tr>
	<td class='byte'>1xxxxxxx</td>
	<td class='byte'>1xxxxxxx</td>
	<td class='byte'>1xxxxxxx</td>
	<td class='byte'>0xxxxxxx</td>
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
* start and end byte of characters can be identified easy and efficiently within a stream of bytes without special knowledge (e.g. about the code-page).

## Code-Page

**NONE** character-codes are arranged on the code page in such a way that the
sequence of bits of a character's bytes (as given in the encoding scheme) 
understood as one unsigned integer is the character code (code point).
A _decoding_ isn't required.

All code points that cannot be encoded in the scheme aren't used. 

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
The above illustrates the distribution of usable <i class='region'> </i> and 
unusable <u class='region'> </u> regions within the first 2 bytes each having
a code space of 128 characters. 
The first region is assigned to the `ASCII` <i class='region ascii'></i> 
character set.

This comb like pattern reoccurs 128 times within the the first 3 bytes in the
second half of its code space. This again reoccurs 128 times within the first
4 bytes and so forth. The `ASCII` region though is an artefact of single byte
characters and special to the first comb. It does not reoccur in later combs.


### Arithmetic's

<table class='big'>
<tr><th></th><th>+</th><th>=</th></tr>
<tr><td>e</td><td>´<td>é</td></tr>
<tr><td>a</td><td>´<td>á</td></tr>
<tr><td>e</td><td>^<td>ê</td></tr>
<tr><td>a</td><td>^<td>â</td></tr>
</table>

