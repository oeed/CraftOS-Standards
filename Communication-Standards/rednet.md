# Rednet #
Rednet is a network protocol for use with modems.
## Rednet Packet ##
A Rednet Packet consists of the following Informations:
type   |   description
------ | --------------------
number | reciever computer ID
number | sender computer ID
string | content
## Transmission ##
The Rednet Message gets transmitted by using the reciever computer ID as channel and the sender computer ID as reply channel. The content gets sent as the message
