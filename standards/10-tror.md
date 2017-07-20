# *COS 10:* Terminal Redirection over Rednet

## Quick information
| Information |                                                                |
| ----------- | -------------------------------------------------------------- |
| Version     | 1.1.0                                                          |
| Type        | Protocol                                                       |

## Technical Details
Terminal Redirection over Rednet, or TRoR, defines a method of broadcasting a
terminal from one computer (the sever) to one client.

The server and client communicate via a series of "packets". Packets are
generally sent with one packet per rednet message, but multiple packets MAY
be sent at once with each being delimited with the line feed (LF) character
(`\n`, ASCII code 10). Consequently, the packet's payload CANNOT contain the LF
character.

Packets are composed of 3 components:

 - A two character packet code. This defines the command to execute. An unknown
   command MUST be discarded.
 - Optional implementation-specific data about the packet. Arbitrary data MAY be
   placed here but SHALL NOT contain a semicolon (`;`) or a LF character. The
   implementation MUST NOT malfunction if data is found here.
 - The packet's payload.

These components are combined in the format:
```
<Code>:<Metadata>;<Payload>
```

The packet MUST take this exact format even if one component is empty. Both
`:` and `;` MUST be present.

### Connection management
The server MAY send packets to the client to handle the connection, such as
determining what extensions to the protocol the client supports.

| Code | Payload         | Description                                         |
| ---- | --------------- | --------------------------------------------------- |
| `SP` | `<extensions>`  | Carries the extensions supported by the server and requests a capability list from the client. Each extension should be surrounded in hyphens. This packet MAY be sent at any time. |
| `SC` | `<message>`     | Closes this connection. The server SHOULD NOT send any more packets after this one, nor handle any incoming packets. |

Some packets require the client to respond.

| Code | Payload         | Description                                         |
| ---- | --------------- | --------------------------------------------------- |
| `SP` | `<extensions>`  | Carries the extensions supported by the client. Each extension should be surrounded in hyphens. This packet MAY be sent at any time and SHOULD be sent whenever a `SP` packet is received. |

### Terminal broadcasting packets
The main purpose of TRoR is to broadcast the terminal state over rednet. The
following packets  are sent from the server to the client to specify actions the
terminal has taken.

| Code | Payload           | Description                                                                 |
| ---- | ----------------- | ----------------------------------------------------------------------------|
| `TW` | `<text>`          | Carries the written text to the client. The LF character should be replaced with a space. |
| `TC` | `<x>,<y>`         | Sets the cursor position on the client screen.                              |
| `TE` | None              | Clears the client's screen.                                                 |
| `TL` | None              | Clears the current line on the client.                                      |
| `TS` | `<count>`         | Scrolls the client screen by a set number of lines.                         |
| `TB` | `<blink>`         | Sets the cursor blink where `true` is blinking and `false` is not blinking. |
| `TF` | `<color>`         | Sets the foreground color.\*                                                |
| `TK` | `<color>`         | Sets the background color.\*                                                |
| `TM` | `<c>,<r>,<g>,<b>` | Sets the palette for colour `c` to use the given RGB values. `r`, `g` and `b` MUST be numbers between 0 and 1. |
| `TR` | `<w>,<h>`         | Sets the size of the client terminal in width and height. The client MAY chose to discard data which does not fit on the screen. |
| `TY` | `<f,b,t>`         | Sets the foreground, background and text of the current line. All three fields MUST be the same length.\*†                       |
| `TV` | `[<f,b,t>:]`      | Sets the entire terminal's contents. Each line is separated by the `:` character and composed of the foreground, background colors and text. All fields across all lines MUST be the same length. |

\* All colors use the codes defined in [COS 4][cospaint]. The client MAY choose
to ignore colors if it is incapable of rendering them.

† All fields being the same length allows the packet parser to read `n`
characters once the first `,` has been found. The implementation SHOULD discard
the packet if each field is not the same length but MAY attempt to recover.

### Client querying commands
The server MAY send packets to the client to determine information about the
client such as color capabilities. The client SHOULD send an appropriate
response packet.

| Code | Payload         | Description                                                     |
| ---- | --------------- | --------------------------------------------------------------- |
| `TQ` | None            | Queries the client for terminal dimensions and color support.   |
| `TG` | None            | Queries the client for the current cursor position.             |
| `TN` | `<c>`           | Queries the client for the current pallet for the given colour. |

The client should send an appropriate response packet to these requests:

| Code | Payload           | Description                                         |
| ---- | ----------------- | --------------------------------------------------- |
| `TI` | `<w>,<h>,<col>`   | Carries the client terminal's width, height and color support to the server. This packet MAY be sent at any time and SHOULD be sent whenever a `TQ` packet is received. |
| `TP` | `<x>,<y>`         | Carries the client terminal's cursor position. This MUST be sent when receiving a `TG` packet and SHOULD NOT be sent at any other time. |
| `TO` | `<c>,<r>,<g>,<b>` | Carries the client terminal's pallete for a given colour. This MUST be sent when receiving a `TN` packet and SHOULD NOT be sent at any other time. |

### Client events
The client MAY send events such as key presses to the client. However the server
MAY ignore these.

| Code | Payload             | Description                                     |
| ---- | ------------------- | ----------------------------------------------- |
| `EV` | `<event,arg1,arg2>` | Queues an event on the server.                  |

The event name and its arguments should be displayed as the appropriate nil,
boolean, string or number literal. Strings must use double quotes and escape the
LF character.

Lua tables MAY be included as an argument, though an implementation is allowed to
discard it. Other Lua expressions such as binary operators or functions MUST NOT
be transmitted and SHOULD NOT be executed.

### Extension: Text table
The text table extension allows sending a serialized version of the terminal
buffer using the TRoR protocol. This buffer contains information about
cursor status, terminal size and terminal contents.

Support of this extension SHOULD be shown by including the `textTable` in the
`SP` packet. This extension MUST NOT be used if the client does not indicate its
support and `TV` should be used instead.

| Code | Payload         | Description                                         |
| ---- | --------------- | --------------------------------------------------- |
| `TT` | `<payload>`     | Sets the entire terminal's state.                   |

The payload should be a serialized table and MUST NOT contain the LF character.
The table MUST contain the following fields:

| Field         | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| `sizeX`       | The width of the terminal. This MUST be an integer.          |
| `sizeY`       | The height of the terminal. This MUST be an integer.         |
| `cursorX`     | The cursor's X position. This MUST be an integer.            |
| `cursorY`     | The cursor's Y position. This MUST be an integer.            |
| `cursorBlink` | Whether the cursor is blinking. This MUST be either `true` or `false`. |
| `text`        | A table representing the textual contents of the terminal.†  |
| `textColor`   | A table representing the background color of the terminal.\*†|
| `backColor`   | A table representing the textual contents of the terminal.\*†|

The table SHOULD contain the following fields. If they are ommitted then the
client SHOULD revert to the default values.
| ------------- | ------------------------------------------------------------ |
| Field         | Description                                                  |
| `palette`     | A table representing the palette of the terminal.‡           |

\* All colors use the codes defined in [COS 4][cospaint]. The client MAY choose
to ignore colors if it is incapable of rendering them.

† Each entry of the table represents a separate line of the terminal. There MUST
be `sizeY` table entries, each being `sizeX` characters long.

‡ This should be a list of values, using the colour codes defined in
[COS 4][cospaint]. Each value MUST be a table with `r`, `g` and `b` table
entries, each being composed of a number between 0 and 1.

## Available Utilities
 - [nsh and its related utilities](https://github.com/lyqyd/cc-netshell/) uses
   TRoR and various extensions to allow interacting with a computer remotely.

[cospaint]: 4-paint.md#color-codes "COS 4: Paintutils Image"
