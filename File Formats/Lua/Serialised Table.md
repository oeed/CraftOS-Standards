# *COS ?:* Lua Serialised Table

## Quick information

| Information |                           |
| ----------- | ------------------------- |
| Type        | Serialised Table          |
| MIME        | `lua/table`               |
| Extensions  | `.tbl`                    |

## Technical details

*This format is based upon [plain text](/File%20Formats/Documents/Plain%20Text.md) and as such technical details that apply to plain text also apply to this format.*

Lua serialised table files must contain a valid Lua table. A serialised table is valid if `textutils.unserialise` parses the *entire* contents of the file in to a table.

It is not strictly necessary to use `textutils.serialise` when creating the file. For example, you can make another function which does the same but omits unnecessary whitespace. The only requirement is that it is *parseable*.

### Example

```Lua
{
	{
		1,
		2,
		3,
		4
	}
	"hello",
	false,
	nil,
	["key"] = "value"
}
```