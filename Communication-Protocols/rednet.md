# Rednet #

Protocol            | Rednet
------------------- | ------------------
transmission method | Modem (Peripheral)
full name           | Rednet
short name          | RN
protocol ID         | rednet

Rednet is a standard protocol included in computercraft.

## Rednet Packet ##

A Rednet Packet consists of the following Informations:

type    | name           | description
------- | -------------- | ---------------------------------------------
number  | nRecipient     | the target computer ID or 65535 for broadcast
number  | nAnswerChannel | sender computer ID
table   | tMessage       | table mentioned below

tMessage table:

type     | name       | describtion
-------- | ---------- | ---------------------------------------------
number   | nMessageID | a random number from 1 to 2147483647
number   | nRecipient | the target computer ID or 65535 for broadcast
any data | message    | the message to be transmitted
string   | sProtocol  | an identifier for a protocol

## Transmission ##

### If nRecipient equals nAnswerChannel ###

The packet stays on the same computer and gets handled as an ingoing packet.

### If sender computer ID doesn´t equal reciever computer ID ###

#### Sending ####

Two modem packages get sent:

field        | value
------------ | --------------------
channel      | nRecipient
replyChannel | nReplyChannel
message      | tMessage


field        | value
------------ | --------------------
channel      | 65533
replyChannel | nReplyChannel
message      | tMessage

#### Repeating ####

A repeater listens to channel 65533 and waits for incoming rednet packets. Everytime it recieves one it looks if it already had transmitted a packet with this nMessageID, if it hasn´t it sends two packets using the same pattern as for a sending task.

#### Recieving ####

A recieving computer listens to the channel whichs number is equal to its Computer ID and on channel 65535. When it recieves one, it checks if it recieved a message with the same nMessageID, if it hasn´t it handles the packet as an ingoing packet.
