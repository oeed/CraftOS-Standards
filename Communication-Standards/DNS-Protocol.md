# Domain Name System #

Information | DNS
----------- | ------------------
is based on | Rednet (Protocol)
full name   | Domain Name System
short name  | DNS
protocol ID | dns

DNS is a Computercraft built-in protocol to handle Host Names. It uses P2P technology to search for computer wich 

## Lookup Packet ##

The lookup packet is a table sended over Rednet with the protocol set to ´dns´

type   | name      | description
------ | --------- | --------------------------
string | sType     | has to be ´lookup´
string | sHostname | the hostname to search for
string | sProtocol | the protocol to search for

## Lookup Respose Packet ##

The lookup response packet is the nesponse to a lookup packet

type   | name      | description
------ | --------- | ---------------------------
string | sType     | has to be ´lookup response´
string | sHostname | the hostname
string | sProtocol | the protocol

## Transmission ##

A lookup packet gets broadcasted via rednet, containing the hostname and the port searching for.

A computer which recieves a lookup packet, checks if it has registered the hostname with the protocol, if it has, it returns the packet with only changing sType to ´lookup response´
