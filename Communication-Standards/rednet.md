# Rednet #

Rednet is a network protocol for use with modems.

## Rednet Packet ##

A Rednet Packet consists of the following Informations:

type    | name           | description
------- | -------------- | ----------------------
number  | nRecipient     | the target computer ID
number  | nAnswerChannel | sender computer ID
table   | tMessage       | table mentioned below

tMessage table:

type     | name       | describtion
-------- | ---------- | ------------------------------------
number   | nMessageID | a random number from 1 to 2147483647
number   | nRecipient | the target computer ID
any data | message    | the message to be transmitted
string   | sProtocol  | an identifier for a protocol

## Transmission ##

### If nRecipient equals nAnswerChannel ###

The packet stays on the same computer and gets handled as an incoming packet.

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
