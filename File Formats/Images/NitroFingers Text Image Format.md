# NitroFingers Text Image

## Quick information

| Information |                                     |
| ----------- | ----------------------------------- |
| Type        | Image file format with text support |
| MIME        | `image/nftext`                      |
| Extensions  | `.nft`                              |

## Technical details

A *NitroFingers Text Image* file can look like this:

```
?0   ?5Hello?2 World
?2       ?5       ?a
?2   ?a ?5        ?a
?2H?7owd?by out   ?a  
?2    ?fther  ?3  ?a
```

Each line represents a line of pixels in the image. Color changes are represented by commands like `?0` which basically means: Change color to `0`. Each space character, the color changing command is followed by, is one pixel in that color. The space characters can be replaced by normal characters as text.

## Color codes

| Code | Color      |
| ---- | ---------- |
| 0    | White      |
| 1    | Orange     |
| 2    | Magenta    |
| 3    | Light blue |
| 4    | Yellow     |
| 5    | Lime       |
| 6    | Pink       |
| 7    | Gray       |
| 8    | Light gray |
| 9    | Cyan       |
| a    | Purple     |
| b    | Blue       |
| c    | Brown      |
| d    | Green      |
| e    | Red        |
| f    | Black      |
