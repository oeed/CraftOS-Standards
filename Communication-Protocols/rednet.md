# Rednet #

Protocol | Rednet
-------- | ------
Transmission Method | Modem (Peripheral)
Full Name | Rednet
Short Name | RN
Protocol ID | `rednet`

Rednet is a standard protocol included in computercraft. It is intented to be used as transmission method for other protocols.

## Rednet Message ##

A Rednet Message consists of the following informations:

Type | Name | Description
---- | ---- | -----------
`number` | `nRecipient` | The target: either a computer ID or `65535` for broadcast
`number` | `nAnswerChannel` | The ID of the computer which created the message
`table` | `tMessage` | Table mentioned below

`tMessage` table:

Type | Name | Describtion
---- | -----| -----------
`number` | `nMessageID` | A random number from `1` to `2147483647`
`number` | `nRecipient` | The target computer ID or `65535` for broadcast
`any data` | `message` | The data to be transmitted, specified by the protocol
`string` | `sProtocol` | Protocol ID of the used protocol
`sProtocol` can also be `nil` but it is **highly recommended to always send a valid Protocol ID in** `sProtocol`

## Transmission ##

### If nRecipient equals nAnswerChannel ###

The message doesn´t leave the computer and gets handled as an ingoing message.

### If sender computer ID doesn´t equal reciever computer ID ###

#### Sending ####

Two modem packages get sent:

Field | Value
----- | -----
`channel` | `nRecipient`
`replyChannel` | `nReplyChannel`
`message` | `tMessage`

Field | Value
----- | -----
`channel` | `65533`
`replyChannel` | `nReplyChannel`
`message` | `tMessage`

#### Repeating ####

A repeater listens to channel `65533` and waits for incoming rednet messages. Everytime it recieves one it looks if it already had transmitted a packet with the same`nMessageID`, if it hasn´t it sends two packets using the same pattern as for a sending task.

**Attention:** `nReplyChannel` *has to be the same as in the incoming message!*

#### Recieving ####

A recieving computer listens to the channel whichs number is equal to its Computer ID and on channel `65535` . When it recieves one, it checks if it recieved a message with the same `nMessageID`, if it hasn´t it handles the packet as an ingoing message.

## Implementations ##

* [Rednet API](http://www.computercraft.info/wiki/Rednet_(API)) (included in CraftOS) (API)
