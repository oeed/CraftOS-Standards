# File Metadata System

## Folder structure

Every folder (including root, discs and empty folders) has a file called *.metadata*. 

For example, consider this file tree:

```
= documents
	- image.ucg
	- readme.txt
	= code
		- paint.lua
= system
	- startup

```

Under this metadata system, the file tree would be as such:

```
- .metadata
= documents
	- .metadata
	- image.ucg
	- readme.txt
	= code
		- .metadata
		- paint.lua
= system
	- .metadata
	- startup

```

It is important to note that any file with the name *.metadata* **must not be given metadata/have metadata stored**.

### Behaviour and Treatment of *.metadata* Files

Essentially, the user should never be able to change or see a *.metadata* file.

*.metadata* files must **always** be hidden, this includes a "show hidden files" option; the user must never see them. It must also be **impossible** for the user to open, edit, remove, move, rename, delete or otherwise mutate the file. It must also be **impossible** for the user to create a folder or file called '.metadata'. `fs.isReadOnly` must return `true`, `fs.open` must return `nil` and `fs.exists` must return `false` for a *.metadata* file and must not appear when using `fs.list`.

## MIME detection

To allow for quick, efficient and reliable MIME detection, each extension can only have ***one*** MIME associated with it. However, one MIME can be associated with multiple extensions. This allows for smooth transitions between metadata supporting systems and non-metadata supporting systems. For example, a format with the MIME `image/jpeg` could use `.jpg`, `.jpeg`, etc. However, `.jpg` can ***only*** be associated with with `image/jpeg`.

*All* of the accepted standardised file formats must have their MIME and extensions detectable by each metadata system.

### Unknown MIME

If the MIME cannot be detected `nil` must be used as value. When loading the metadata of a file where the MIME is `nil` you must always try to redetect its MIME.
## Metadata file contents

The information in the *.metadata* file is the metadata for the folder itself and the files within the folder.

The file is a binary file with data in sections. There is one section for each file in the folder. Sections are delimited by a null byte `\0` at the end of each section (including the last section).

### Section

#### Section Components

*All integers are big endian.*

**`String`**: A string begins with an unsigned 8-bit integer indicating the length *n* (number of booksytes). The following *n* bytes must be the characters of the string. A `nil` value is stored as a string of zero length.

**`Timestamp`**: A timestamp is stored as signed 32-bit integer with a Unix timestamp. Timestamps must use UTC time, not the local timezone. If the timestamp is unknown, `1451606400` should be used as a default value (00:00 1/1/2016).

**`Int8`**: An unsigned 8-bit integer.

**`Icon`**: An icon begins with an unsigned 16-bit integer indicating the length *n* (number of bytes). The following *n* bytes are the contents of an icon in ** format. Do not abuse this value and avoid relying on it too heavily.

**`Key`**: A key (as in key-value) in a single byte, it should be a single ASCII character.

**`Value`**: A `String`, `Timestamp`, or `Icon`.

**`Key-Value Pair`**: A key-value pair begins with a `Key` and is immediately followed by a `Value`.

#### Section Definition

A section begins with a `String`, the complete file name (not path) of the file. The metadata for the folder is stored under the name '.metadata'. For example, 'image.ucg'.

The remaining bytes until a null byte make up one or more `Key-Value Pairs`.

When a null byte is reached a new section begins.

### Keys

The values listed below must **always** use the assigned `Key`. Values that are not italicised are **required** and must be specified for every file.

|      Value       | Key | Value Type  |
| ---------------- | --- | ----------- |
|      MIME        |  T  |  `String`   |
| Date Last Opened |  O  | `Timestamp` |
|  Date Modified   |  M  | `Timestamp` |
|  Date Created    |  C  | `Timestamp` |
|  *Custom Icon*   | *I* |  *`Icon`*   |
|     *Author*     | *A* | *`String`*  |
|    *Version*     | *V* |  *`Int8`*   |

It it **completely prohibited** to use any key not listed above or use an incorrect `Value`.

### Example

*Note: Each individual group of bytes is placed in a code block.*

Folder structure:

```
= documents
	- .metadata
	- readme.txt
```

The contents of .metadata would be as follows, totalling 94 bytes:

`0x09` `.metadata` *The start of the 'documents' folder's section.* 

`T` `0x15` `application/directory` *The 'documents' folder's MIME.*

`M` `0x56976742` `C` `0x56975C44` `O` `0x56976742` *The 'documents' folder's timestamps and author.*

`0x00`  *The null byte, indicating the end of the section.*

`0x0A` `readme.txt` `T` `0x0A` `plain/text` `M` `0x56976014` `C` `0x56975C00` `O` `0x56978624` `A` `0x04` `oeed` `0x00`  *The entire 'readme.txt' section.*

You can download this example file [here](http://puu.sh/mvdqC/41d3b5151f).