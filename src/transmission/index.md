# Transmission layer

This layer is responsible for the connection between two directly connected nodes.
It has no knowledge of the global state and lives directly above the choosen transport layer.

Sequence
Permanent
type
receiver

## ?????????

This section describes the format of packets to be send over the network.
It does not specify the format of the content of the packets, but the metadata of the packets.
This metadata is used in routing the packets around.

The the metadata part has a fixed length of `xxxx` bytes.
It contains the following parts:

- magic byte (4 byte, `0x20f57c03`)
- reserved (3 bit)
- data length (2 byte)
- data
- signature (8 byte, ED25519)

SYN/ACK?

```
| 4 bytes    | 4 bits  | 4 bits |
+------------+---------+--------+
| Magic byte | Flags   | TTL    |
+------------+---------+--------+
```

## Magic byte

This magic byte is four bytes long, and fixed at `0x20f57c03`.
Any packet which don't start with this magic byte can safely be ignored.
It is added to makes sure you are dealing with an actual packet, instead of random noise.

## Flags

The first meaningfull part of a packet are the flags.
Flags are a single bit datatype where `1` equals `true` and `0` equals `false`.
These flags help with parsing the packet, as not all packet have the same format.
In total there are 4 flags, but not all of them are in use.
Flags are processed as they come in, so the left most flag is flag 0.

```
| Flag ID | Name                    |
| ------- | ----------------------- |
| 0       | Reserved for futher use |
| 1       | Reserved for futher use |
| 2       | Reserved for futher use |
| 3       | Reserved for futher use |
```

## TTL

The TTL or time to live is an essential part of preventing flooding of the network.
Every message starts with a hop count between `1` and `15`.
At each hop the TTL counter is reduced by `1`.
A received packet should not be retransmitted if the TTL is `0` after substracting the counter.
It should still be processed like a normal packet.

## Underlying transport

While UDP is recommended for this network, it is not limited to it.
If you want you can also use other transport protocols like TCP, TLS, WS and any other type of socket connection.
