# File Formats

File formats are specific ways to store data that can be read and written using standardised methods.

## Proposal Requirements

Every format must specify all of the following:

### File Extension

Example: `.lua`

If the file format is new it must only be given extension; there's no point have 3 different extensions for the same file.

If the file format is an existing format *and it already* uses multiple extensions then you should list all of the commonly used ones.

### MIME

Example: `text/lua`, `image/sketch`, `silica/theme`

Every file format must be given ***one*** MIME. If more than one already exists pick **one**.

A MIME should tell a program exactly what format the file is, so it must be unique for each format. Having multiple MIMEs for one file format creates situations where some programs will assume they do not support the format, even if they do.

MIMEs should follow the standards given by the [IANA](http://www.iana.org/assignments/media-types/media-types.xhtml). For example, all image formats should follow the format used by desktop image formats such as PNG.

It is acceptable to create your category (bit before the slash). For example, Silica has over 9 different file formats, all of which start with `silica/`.

### Code to Read and Write

You must create either an API, or if, the code is not very long, example code, to read and write your file format so others do not have to. However, your description of the format should be thorough enough for someone to do so without the API/example code.