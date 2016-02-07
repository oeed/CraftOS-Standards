# Rednet #

Rednet is a network protocol for use with modems.

## Rednet Packet ##

A Rednet Packet consists of the following Informations:

type    | name           | description
------- | -------------- | ---------------------
number  | nRecipient     | reciever computer ID
number  | nAnswerChannel | sender computer ID
string  | tMessage       | table mentioned below

## Transmission ##

### If sender computer ID equals reciever computer ID ###

The packet stays on the same computer and gets handled as an incoming packet.

### If sender computer ID doesn´t equal reciever computer ID ###

#### Sending ####

Two modem packages get sent:

field        | value
------------ | --------------------
channel      | reciever computer ID
replyChannel | sender computer ID
message      | content


field        | value
------------ | --------------------
channel      | 65533
replyChannel | sender computer ID
message      | content
