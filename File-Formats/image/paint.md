# *COS 4:* Paintutils Image

## Quick information

| Information |                           |
| ----------- | ------------------------- |
| Type        | Image file format         |
| MIME        | `image/paint`             |
| Extensions  | `.nfp`                    |

## Technical details

The file contains a row of one character long values as pixel information. Each pixel of one row is put directly behind another in the corresponding line one of these values.

```
0f0f0f0f
0000000f
00000000
  9abc    
12345678
```

This is an example of an image file being opened with a text editor. Each value maches one pixel. The values always have to be one of the 16 color codes (0-9, a-f).
Having a space as a pixel information makes that pixel transparent.

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
|      | Transparent|
