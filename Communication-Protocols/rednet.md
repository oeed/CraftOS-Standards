# Rednet #

protocol | Rednet
-------- | ------
transmission method | Modem (Peripheral)
full name | Rednet
short name | RN
protocol ID | `rednet`

Rednet is a standard protocol included in computercraft. It is intented to be used as transmission method for other protocols.

## Rednet Message ##

A Rednet Message consists of the following informations:

type | name | description
---- | ---- | -----------
number | `nRecipient` | the target: either a computer ID or `65535` for broadcast
number | `nAnswerChannel` | the ID of the computer which created the message
table | `tMessage` | table mentioned below

`tMessage` table:

type | name | describtion
---- | -----| -----------
number | `nMessageID` | a random number from `1` to `2147483647`
number | `nRecipient` | the target computer ID or `65535` for broadcast
any data | `message` | the data to be transmitted, specified by the protocol
string | `sProtocol` | protocol ID of the used protocol
`sProtocol` can also be `nil` but it is **highly recommended to always send a valid Protocol ID in** `sProtocol`

## Transmission ##

### If nRecipient equals nAnswerChannel ###

The message doesn´t leave the computer and gets handled as an ingoing message.

### If sender computer ID doesn´t equal reciever computer ID ###

#### Sending ####

Two modem packages get sent:

field | value
----- | -----
`channel` | `nRecipient`
`replyChannel` | `nReplyChannel`
`message` | `tMessage`

field | value
----- | -----
`channel` | `65533`
`replyChannel` | `nReplyChannel`
`message` | `tMessage`

#### Repeating ####

A repeater listens to channel `65533` and waits for incoming rednet messages. Everytime it recieves one it looks if it already had transmitted a packet with the same`nMessageID`, if it hasn´t it sends two packets using the same pattern as for a sending task.

**Attention:** `nReplyChannel` *has to be the same as in the incoming message!*

#### Recieving ####

A recieving computer listens to the channel whichs number is equal to its Computer ID and on channel `65535` . When it recieves one, it checks if it recieved a message with the same `nMessageID`, if it hasn´t it handles the packet as an ingoing message.

## APIs ##

* [Rednet API](http://www.computercraft.info/wiki/Rednet_(API)) (included in CraftOS)
