# *COS 2:* Lua Program

## Quick information

| Information |                           |
| ----------- | ------------------------- |
| Type        | Lua Program               |
| MIME        | `lua/program`             |
| Extensions  | `.prg`, `.lua` *See '.lua extension'*|

## Technical details

*This format is based upon [plain text](/File%20Formats/Documents/Plain%20Text.md) and as such technical details that apply to plain text also apply to this format.*

A Lua program file *must* contain valid Lua code which will immediately execute code upon being run, rather than simply returning data or loading functions. There is no requirement for a 'program' to have any user interaction or utilise the screen, but to simply *run* code rather than *load* it.

### Note: Usage of `.lua` extension

A file with the `.lua` extension by default should be assumed to be a Lua program, not any other type of Lua file. However, you should never use the `.lua` extension when creating new files unless the user manually specifies it.