# *Protocol Name*

placeholder | *Protocol Name*
------------|----------------
Protocol Type | *P2P/Client-Server*
Identifier String | *the identifier inside a inline code formating element*

*some basic information like intended use*

## Usage

*an exact explanaiton of the protocol, referring to the packets using links, can be splitted into parts*

## Packets

*a list of all packets using the following sheme:*

### *Packet Name* Packet

*the packet definition inside a block code formitting element: the type of the packet/message (string, number, table, ...) then a name for it and if it isn´t a table either three dashes and an explanation or an equal sign and a value. If it is a table use a doublepoint and write its contents using the same notation under it, but 3 spaces intended. Examples:*
```
string sMessage --- the message
```
*this one is just a string as packet*
```
table tMessage :
   string sType = "foo"
   boolean bTest --- a completely useless boolean
```
*this one is a table containing a string at index "sType" which has to contain foo and a boolean at index "bTest"*
