# CraftOS Terminology Reference

|   Information  |                |  
|----------------|----------------|
| Version        | 1.0.0          |  
| Type           | Miscellaneous  |
| MIME           | Not applicable |
| File Extension | Not applicable |

### Contents

1. **Abstract**  
2. **Data storage**  
	2.1 **Integers**  
	&emsp;2.1.1 **Octet**  
	&emsp;2.1.2 **Word**  
	&emsp;2.1.3 **Double Word**  
	&emsp;2.1.4 **Quad Word**  
	2.2 **Strings**  
	2.3 **Floats**  
3. **General**  
	3.1 **Executable**  
	3.2 **Library**  
	3.3 **Resource**  
	3.3 **API**

### 1. Abstract

This document defines standard terminology for use when writing a standard. Whenever a standard uses a term defined in this document, it must link back here. Whenever a standard uses a term not defined in this document, it must provide appropriate explanation.

This standard does not cover terms that are implicit to the context or too simple: things like _computer_ and _file_, in a ComputerCraft context, have a meaning set in stone, and there is no need to reiterate.

### 2. Data Storage

This section of the document specifies terms regarding how data is laid out in memory, or stored in a mass storage device.

#### 2.1. Integers

#### 2.1.1. Octets
_also acceptable: octads_  
_not acceptable: bytes_


Octets are 8-bit-wide numbers, ranging from -127 to 127 when signed or from 0 to 255 when unsigned.

##### 2.1.2. Words
_not acceptable: short_  

A word is comprised of two octets (16 bits), ranging from -32,768 to 36,768 when signed or from 0 to 65535.

#### 2.1.3. Double Words
_also acceptable: ints_

A double word, double (not to be confused with an [IEEE 754](https://en.wikipedia.org/wiki/IEEE_floating_point) double precision floating point) or int is comprised of two words (32 bits), ranging from -2,147,483,647 to 2,147,483,647 when signed or from 0 to 4,294,967,295 when unsigned.

**Note**: while technically correct, the use of _double_ to mean _double word_ can entail some ambiguity, as _double_ can also mean an [IEEE 754](https://en.wikipedia.org/wiki/IEEE_floating_point) double precision floating point. See section 2.3 for further details.


#### 2.1.3. Quad Words
_also acceptable: longs, quads_

A quad word, long int or quad is comprised of two double words, ranging from -9.22337203685478 × 10¹⁸ to 9.22337203685478 × 10¹⁸ when signed or from 0 to 1.84467440737096 × 10¹⁹ when unsigned.

### 2.2. Strings

A string is a sequence of octets, layed out in memory sequentially from the first character to the last character, then followed by a `NUL` (ASCII 0, `\0`) to signify the end of the string.

Strings are always encoded in UTF-8 (but are limited to the ASCII range), without byte-order marks.

**Printable strings** are a subset of strings that only contain characters in the printable ASCII range.

### 2.3. Floats

Floating-point numbers (floats, for short) refer [IEEE 754](https://en.wikipedia.org/wiki/IEEE_floating_point)  double-precision floating points unless explicitly stated otherwise.


### 3. General

#### 3.1. Executable

An executable is a file containing Lua (or otherwise) that can be loaded by CraftOS (or otherwise) and executed. Most executables are user-facing applications.

#### 3.2. Library

A library is a file containing Lua (or otherwise) that can be loaded by CraftOS (or otherwise) and used for code reusal. Do not the difference between an API and a library.


#### 3.3. Resource

A resource is a file containing Lua (or otherwise) that can be loaded by a program or library, but is neither executable code or library code. Resources are typically images, but can also be localization strings or configuration files.

#### 3.4. API

An API (application programming interface) is similar, but different, from a library. Whereas a library contains actual code for performing tasks, an API is just a description of the interface a library exposes. An API can be public, for use in application development with the library, or private, for use in internal development of the library itself.
