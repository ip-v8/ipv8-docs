# Transmission layer

This layer is responsible for the connection between two directly connected nodes.
It has no knowledge of the global state and lives directly above the choosen transport layer.
It deals with the different types of packets.

Permanent
type
receiver

## Packet types

There are a few different types of packets, to make sure it arrives at the right spot.

- Send
- Ack

The send packet is used to transmit a packet directly between two nodes.
The ack packet is used to acknowledge the receiving of the packed, identified by the sequence ID.
If the ack packet is not received after a certain timeout the sender should resend the packet.
If after `x` amount of tries it still does not respond the node should be marked as failed.
The packet should be rerouted trough a different node if possible, if not drop the packet.
A higher layer will do a retransmittion of the packet starting from the source.

## Packet format

This section describes the format of packets to be send over the network.
It does not specify the format of the content of the packets, but the metadata of the packets.
This metadata is used in routing the packets around.

It contains the following parts:

- magic byte (4 byte, `0x20f57c03`)
- sequence ID (2 bit)
- reserved (3 bit)
- data length (2 byte)
- data (x byte)
- signature (8 byte, ED25519)

SYN/ACK?

```
| 4 bytes    | 4 bits  | 4 bits |
+------------+---------+--------+
| Magic byte | Flags   | TTL    |
+------------+---------+--------+
```

## Magic byte

This magic byte is four bytes long, always set to `0x20f57c03`.
Any packet which don't start with this magic byte can safely be ignored, as this would be a different protocol.
It is added to makes sure you are dealing with an IPv8 packet, instead of something else (non-malicious).

## Flags

The first meaningfull part of a packet are the flags.
Flags are a single bit datatype where `1` equals `true` and `0` equals `false`.
These flags help with parsing the packet, as not all packet have the same format.
In total there are 4 flags, but not all of them are in use.
Flags are processed as they come in, so the left most flag is flag 0.

```
| Flag ID | Name                    |
| ------- | ----------------------- |
| 0       | Real time               |
| 1       | Reserved for futher use |
| 2       | Reserved for futher use |
| 3       | Reserved for futher use |
```

### Real time

If the packet is real time

## Underlying transport

While UDP is recommended for this network, it is not limited to it.
If you want you can also use other transport protocols like TCP, TLS, WS and any other type of socket connection.
