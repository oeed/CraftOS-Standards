# *COS 10:* Terminal Redirection over Rednet

## Quick information
| Information |                                                                |
| ----------- | -------------------------------------------------------------- |
| Version     | 1.0                                                            |
| Type        | Protcol                                                        |

### Technical Details
Terminal Redirection over Rednet, or TRoR, defines a method of broadcasting a
terminal from one computer (the sever) to one client.

The server and client communicate via a series of "packets". Packets are
generally sent with one packet per rednet message, but multiple packets MAY
be sent at once with each being deliminated with the line feed (LF) character
(`\n`, ASCCI code 10). Consequently, the packet contents CANNOT contain the LF
character.

Packets are composed of 3 components:

 - A two character packet code. This defines the command to execute. An unknown
   command MUST be discarded.
 - Optional implementation-specific data about the packet. Arbitary data MAY be
   placed here but SHALL NOT contain a semicolon (`;`) or LF character. The
   implementation MUST NOT malfunction if data is found here.
 - The main packet contents.

These components are combined in the format:
```
<Packet code>:<Metadata>;<Packet contents>
```

#### Terminal broadcasting packets
The main purpose of TRoR is to broadcast the terminal state over rednet. The
following packets  are sent from the server to the client to specify actions the
terminal has taken.

| Code | Packet contents | Description                                                                 |
| ---- | --------------- | ----------------------------------------------------------------------------|
| `TW` | `<text>`        | Carries the written text to the client. The LF character should be replaced with a space. |
| `TC` | `<x>,<y>`       | Sets the cursor position on the client screen                               |
| `TE` | None            | Clears the client's screen                                                  |
| `TL` | None            | Clears the current line on the client                                       |
| `TS` | `<count>`       | Scrolls the client screen by a set number of lines.                         |
| `TB` | `<blink>`       | Sets the cursor blink where `true` is blinking and `false` is not blinking. |
| `TF` | `<color>`       | Sets the foreground color.\*                                                |
| `TK` | `<color>`       | Sets the background color.\*                                                |
| `TR` | `<w>,<h>`       | Sets the size of the client terminal in width and height. The client MAY chose to discard data which does not fit on the screen. |
| `TY` | `<f,b,t>`       | Sets the foreground, background and text of the current line. All three fields MUST be the same length.\*†                       |
| `TV` | `[<f,b,t>:]`    | Sets the entire terminal. Each line is separated by the `:` character and composed of the foreground, background colors and text. All fields across all lines MUST be the same length. |

\* All colors use the codes defined in [COS 4][cospaint]. The client MAY choose
to ignore colours if it incapible of rendering them.

† All fields being the same length allows the packet parser to read `n`
characters once the first `,` has been found. The implementation SHOULD discard
the packet if each field is not the same length but MAY attempt to recover.

#### Client querying commands
The server MAY send packets to the client to determine information about the
client such as color capabilities. The client SHOULD send an appropriate
response packet.

| Code | Packet contents | Description                                                   |
| ---- | --------------- | ------------------------------------------------------------- |
| `TQ` | None            | Queries the client for terminal dimensions and color support  |

The client SHOULD send an appropriate response packet to these requests:

| Code | Packet contents | Description                                                               |
| ---- | --------------- | ------------------------------------------------------------------------- |
| `TI` | `<w>,<h>,<col>` | Send the client terminal's width, height and color support to the server. |

#### Client events
The client MAY send events such as key presses to the client. However the client
MAY ignore these.

| Code | Packet contents     | Description                                     |
| ---- | ------------------- | ----------------------------------------------- |
| `EV` | `<event,arg1,arg2>` | Queue an event on the server.                   |

The event name and its arguments should be displayed as the appropriate nil,
boolean, string or number literal. Strings must use double quotes and escape the
LF character.

Lua tables MAY be included as an argument, though an implementation is allowed to
discard it. Other Lua expressions such as binary operators or functions MUST NOT
be transmitted and SHOULD NOT be executed.

#### Available Utilities
 - [nsh and its related utilities](https://github.com/lyqyd/cc-netshell/) does things
   differently.

[cospaint]: /File-Formats/image/paint.md "COS 4: Paintutils Image"