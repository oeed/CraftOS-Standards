# **Universal Compressed Graphics file format version 3**

## Contents
1. **Abstract**
2. **Quick Overview**
3. **Introduction & Purpose**
4. **Specification**
	4.1 Definitions
	&emsp;4.1.1 ColorValue
	&emsp;4.1.2 LengthValue
	&emsp;4.1.3 HuffmanTree
	&emsp;4.1.4 PixelData
5. **Explanation**
	5.1 Signature
	5.2 version
	5.3 Flags
	5.4 Width
	5.5 Height
	5.6 ColorHuffmanTree
	5.7 LengthHuffmanTree
	5.8 PixelData
	5.9 Huffman Codes
6. **See Also**

## 1. Abstract
This COS (CraftOS Standard) defines and explains a file format for storing images and graphics, specificated for the usage with ComputerCraft and CraftOS 2.

## 2. Quick Overview

| Name       | Value             |
| ---------- | ----------------- |
| Type       | Image file format |
| MIME       | ``image/ucg``     |
| Extensions | ``.ucg``          |

## 3. Introduction & Purpose
The purpose of this file format is to store bitmaps as compact as possible, but still being relatively fast to decompress. To achieve this, the format uses a combination of Huffman Code & run-length encoding. Tests show that a normal image stored using UCG is about 10-40% the size of the same image stored using the ComputerCraft paintutils format. Familiarity with the technique of Huffman Codes is required to create a working encoder, but not necessarily required (still, very helpful & recommended) to understand this Specification.

## 4. Specification
**UCGFile** = FileHeader + ImageHeader + ImageData

FileHeader = Signature + Version
Signature = *(3 bytes)* 0xFF2137
Version = *(1 byte)* 0x03

ImageHeader = Flags + Width + Height
Flags = *(1 byte)*
Width = *(1 word)*
Height = *(1 word)*

ImageData = ColorHuffmanTree + LengthHuffmanTree + PixelData
ColorHuffmanTree = *(HuffmanTree with value type ColorValue)*
LengthHuffmanTree = *(HuffmanTree with value type LengthValue)*
PixelData = *(PixelData)*

### 4.1 Definitions
Bytes stored within a computer do not have a "bit order", since they are always treated as a unit. However, a byte considered as an integer between 0 and 255 does have a most- and least-significant bit, and since we write numbers with the most-significant digit on the left, we also write bytes with the most-significant bit on the left.

In the diagram below, we number the bits of a byte so that bit 0 is the least-significant bit, i.e., the bits are numbered:
```
+--------+
|76543210|
+--------+
```
The bits are processed from the left to the right.

Within a computer, a number may occupy multiple bytes. All multi-byte numbers in the format described here are stored with the most-significant byte first (at the lower memory address). For example, the decimal number 520 is stored as:
```
0        1
+--------+--------+
|00000010|00001000|
+--------+--------+
^        ^
|        |
|        + less significant byte = 8
+ more significant byte = 2 x 256
```
Word: 2 byte / 16 bit binary number

#### 4.1.1 ColorValue
A data element with the type "ColorValue" is a 5bit binary number, storing the numbers 0-32.
If x (the value of this 5bit number) less than 16, you can get the color by just calculating 2^x.
If x equals 16, the object it is associated with is transparent. (In this case, the pixel/pixel row is transparent)
Other values are unused and reserved for later usage.

#### 4.1.2 LengthValue
A data element with the type "LengthValue" is a dynamically-sized binary number, storing the numbers 0-65535.
The first part of a LengthValue is a 4bit number.
If this 4bit number x is less than 13, it equals the value of it. (with value is meant the value that a function reading a LengthValue would return)
If x equals 13, a 5bit number follows that describes the value.
If x equals 14, a 8bit number follows that describes the value.
If x equals 15, a 16bit number follows that describes the value.
The diagram below may explain this better:

| value of the first 4bit Number | the number that follows |
| ------------------------------ | ----------------------- |
| 1, 2, 3, ... 10, 11, 12        | none                    |
| 13                             | a 5bit number           |
| 14                             | a 8bit number           |
| 15                             | a 16bit number          |

Here's an example function that would read a LengthValue:

```lua
function readLengthValue(inputstream)
	local firstNumber = inputstream.readNumber(4)
		-- the argument of the readNumber function specifies how many bits to read
	if firstNumber < 13 then
		return firstNumber
	elseif firstNumber == 13 then
		-- value 13 means that a following 5bit number describes the value
		return inputstream.readNumber(5)
	elseif firstNumber == 14 then
		-- value 14 means that a following 8bit number describes the value
		return inputstream.readNumber(8)
	elseif firstNumber == 15 then
		-- value 15 means that a following 16bit number describes the value
		return inputstream.readNumber(16)
	end
end
```

If a number follows after the first 4bit number, it describes the value. If not, the 4bit number describes the value.

#### 4.1.3 HuffmanTree
Huffman Trees are encoded & serialized using a simple algorithm.
Consider the following Huffman Tree:
```
.     /\
     /  \
    /    \
   /\     B
  /  \
 /    \
A     /\
     /  \
	/    \
   D      C
```

Encoded with UCG's algorithm, it would look like this:
```
0,
0, 1:B,
1:A, 0,
1:D, 1:C
```
Every entry of this list, so for example 1:B, 1:C or 0 is called an element. The Huffman Tree consists purely of these elements. An element can either be a node (written as a 0 in this example) or a leaf (written as 1:B or 1:A, etc in this example).

The first bit of every element describes if this element is a node or a leaf. If this first bit is 0, the element is a node; if the first bit is 1, the element is a leaf. Only if the element is a leaf, a value follows. (in UCG, either a ColorValue or a LengthValue, depending on the Huffman Tree you're currently reading/writing (see section 4))
The Huffman tree encoding algorithm works by going down the Huffman Tree level by level, from the top to the bottom, and writing the elements of the cur- rent level from the left to the right. The number of elements in the next level is 2 times the number of nodes in the level before.

In the example above, the algorithm would start with the root of the Huffman Tree, which is a node; so it writes the bit 0. It then goes to the next level, where it finds a node on the left, and a leaf with the value B on the right. So it writes a 0, then a 1 followed by the binary value of B. In the next level, it finds a leaf with the value A and a node, so it writes a 1 followed by the binary value of A and a 0. Finally, it gets to the last level, where it finds a leaf with value D and a leaf with value C, so it encodes a 1 followed by the binary value of D and another 1 followed by the binary value of C.

The Decoder is now able to completely reconstruct the Huffman Tree, and is able to get the Huffman Code of each value by going down the branches (the left/first branch is the branch with the zero, the right/second branch is the branch with the one). In some rare cases, the root element (so the first element of the whole encoded Huffman Tree) is a leaf. This means that its value is assigned a Huffman Code of zero length, and no elements follow. If you were to decode a Huffman Code of this type, you don't do it, because you can automatically assume that the value equals the one given in the root element.

The Huffman Codes of the above example would look like this:

| Value | Huffman Code |
| - | -- |
| A | 00 |
| B | 1 |
| C | 011 |
| D | 010 |

With this tree:
```
.      /\
      /  \
     /    \
    /     /\
   /     /  \
  /     / \  \
 /\    /\  \  \
7  8  9  A  B  0
```
the serialization would look like this:
```
0,
0, 0,
1:7, 1:8, 0, 1:0,
0, 1:B,
1:9, 1:A
```

The Huffman Codes of this example would look like this:

| Value | Huffman Code |
| ----- | ------------ |
| 7 | 00 |
| 8 | 01 |
| 9 | 1000 |
| A | 1001 |
| B | 101 |
| 0 | 11 |

An example HuffmanTree decoder written in lua would look like this:
```lua
function readHuffmanTree(inputstream, readValue)
	if readBit() == 1 then
		-- return the value and a boolean that
		--   marks that there is only 1 element in this tree
		return readValue(), true
	end
	local codes, toread, toread2 = {}, {0}
	local c0, c1

	while #toread > 0 do
		toread2 = {}

		for a = 1, #toread do
			huffmancode = toread[a]
			c0, c1 = {unpack(huffmancode)}, {unpack(huffmancode)}
			c0[#c0+1] = 0
			c1[#c1+1] = 1

			if readBit() == 1 then
				codes[c0] = readValue()
			else
				toread2[#toread2 +1] = c0
			end

			if readBit() == 1 then
				codes[c1] = readValue()
			else
				toread2[#toread2 +1] = c1
			end
		end
		toread = toread2
	end
	return codes
end
```

#### 4.1.4 PixelData
PixelData is an array that consists purely of LengthElements. Each LengthElement consists of a color Huffman Code, encoded in the color Huffman Tree (see section 4), followed by a length Huffman Code, which is encoded in the length Huffman Tree (see section 4). The value of the color Huffman Code equals the color of the array of pixels that this LengthElement describes, while the value of the length Huffman Code equals the number of pixels that this LengthElement describes.

Let's assume we have the following LengthElement:
{4, 31}
This means that 31 pixels with the color "4" follow after the current position. To know if you should switch to the next line, you add the lengths of every LengthElement in the current line together and check if it equals the Width of the image. If it does, the following LengthElements describe the next line of the image.
In cases where the root element of a Huffman Tree is a leaf, there is no entry of this type. For example, if the root element of the color Huffman Tree is a leaf, no LengthElement in the PixelData has a color attribute and only consists of a length attribute. (in this case, the length attribute would equal the width of the image every time, and the LengthTree would only consist of one element, which means that you don't need to write any LengthElement at all, and there is no content in the PixelData block at all.)

If you finished encoding the PixelData and the total number of bits of the file is not divisible by 8, a series of zeroes or ones follows to fill up the last byte.

## 5. Explanation
### 5.1 Signature
The signature (hex number 0xFF2137) is included in the file to check if this file is really in UCG format. Every UCG file of every version has this 3 byte signature at the start of the file.
### 5.2 Version
The version (0x03 = decimal 3) describes the UCG version used to encode this file. Every UCG file of every version has this 1 byte version record following after the signature.
For UCGv2 files, a 2 would be there. This specification **only** describes how to decode UCGv3 images. In case you read a file where this version byte equals 2,
this specification is completely useless.
### 5.3 Flags
The Flags byte is currently unused.
### 5.4 Width
This 2 byte number describes the width (in pixels) of the image.
### 5.5 Height
This 2 byte number describes the height (in pixels) of the image.
### 5.6 ColorHuffmanTree
A Huffman Tree (see section 4.1.3) that assigns every color its Huffman Code for usage in the PixelData block. The values of this Huffman Tree are encoded as ColorValues. (see section 4.1.1)
### 5.7 LengthHuffmanTree
A Huffman Tree (see section 4.1.3) that assigns every length its Huffman Code for usage in the PixelData block. The length values are a result of the RLE (Run-length encoding) done by the encoder. The values of this Huffman Tree are encoded as LengthValues. (see section 3.1.2)
### 5.8 PixelData
This is the block that contains the real content of the image. This makes the biggest part of the file.
### 5.9 Huffman Codes
Huffman Codes are individually sized binary codes.
The technique of Huffman Coding assigns more common used values a shorter Huffman Code and less used values a longer Huffman Code in order to optimize the file size.

An easy example: The character "A" gets used 10 times in a file, the character "B" gets used 3 times and the character "C" 1 time. A character is 1 byte large, so you would need 14bytes to store this without any encoding.
The question is now: Is there a way to store the same information more efficiently? The answer is: Yes, using Huffman Coding. I'm not going to explain here how to get the Huffman Codes of the individual characters, since there is a lot of information in the internet about this topic and this is just a specification of the UCG file format. Huffman Coding would assign the character A the Huffman Code "0", the character B the Huffman Code "10" and the character C the Huffman Code "11".
The total size of the file (without the Huffman Tree that has to written first, so that the decoder knows the Huffman Codes) using these codes would be 18 bits. Using the Huffman Tree serialization algorithm UCG uses, the Huffman Tree would take 29bits. That makes a total of 47bits, or about 6bytes.
## 6. See Also
The official implementation of the UCGv3 file format: https://github.com/ardera/libucg
The CraftOS Standards Repository: https://github.com/oeed/CraftOS-Standards

If you have any questions:
Author's E-Mail Address: ardera@web.de
Author's ComputerCraft forums account: http://www.computercraft.info/forums2/index.php?/user/2015-ardera/
