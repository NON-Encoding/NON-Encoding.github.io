---
layout: default
title:  "NON-Encoding"
---

# *N*ull *O*r *N*ext*-E*ncoding

**NONE** is a variable-length character encoding and code-page standard. 

## Principles
1. Each character is identified by a single code, its character-code.
2. Any character-code is encoded as a sequence of one or more bytes.
3. If the MSB of a byte is `1` the character-code continues.
4. If the MSB of a byte is `0` it is the last byte of a character-code.
5. The bytes and bits are in Big-Endian order.

## Encoding

<table class='encoding'>
<tr>
	<th>Byte 1</th>
	<th>Byte 2</th>
	<th>Byte 3</th>
	<th>Byte 4</th>
</tr>
<tr>
	<td>0xxxxxxx</td>
	<td></td>
	<td></td>
	<td></td>
</tr>
<tr>
	<td>1xxxxxxx</td>
	<td>0xxxxxxx</td>
	<td></td>
	<td></td>
</tr>
<tr>
	<td>1xxxxxxx</td>
	<td>1xxxxxxx</td>
	<td>0xxxxxxx</td>
	<td></td>
</tr>
<tr>
	<td>1xxxxxxx</td>
	<td>1xxxxxxx</td>
	<td>1xxxxxxx</td>
	<td>0xxxxxxx</td>
</tr>
<tr>
	<th colspan="4">...</th>
</tr>
</table>

## Code-Page

<div class='page'>
<i class='ascii byte1'></i><u class='byte1'></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u><u></u>
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


### Arithmetics

<table class='big'>
<tr><th></th><th>+</th><th>=</th></tr>
<tr><td>e</td><td>´<td>é</td></tr>
<tr><td>a</td><td>´<td>á</td></tr>
<tr><td>e</td><td>^<td>ê</td></tr>
<tr><td>a</td><td>^<td>â</td></tr>
</table>

