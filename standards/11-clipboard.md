# *COS 11:* Clipboard

## Quick information
| Information |                                                                                        |
| ----------- | -------------------------------------------------------------------------------------- |
| Version     | 1.0.0                                                                                  |
| Type        | Protocol                                                                               |

### Technical Details
Clipboard defines a method to share information like text with other programs.

It is a Table called "clipboard" in the Shell Environment.

#### The Clipboard Table
It is a Table called "clipboard" in the Shell Environment.

| Header      | Description                                                                            |
| ----------- | -------------------------------------------------------------------------------------- |
| type        | A String, that Describes, what is in the Clipboard (see at Point "Types")              |
| content     | This is the Content of the Clipboard see "Types"                                       |                                                    |

#### Types
| Type        | Content                                                                                |
| ----------- | -------------------------------------------------------------------------------------- |
| text        | Just normal text provided as a String.                                                 |
| nfp         | A nfp Image provided as String                                                         |
| nft         | A nft Image provided as String                                                         |

### Usage
Set text of Clipboard:
```lua
clipboard = {type="text",content="Hello World"}
```
Get Text of Clipboard
```lua
if type(clipboard) == "table" then
    if clipboard.type == "text" then
        print(clipboard.content)
    end
end
```
