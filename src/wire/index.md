# Wire protocol

This section describes the general wire protocol.
It does not define the communities, but they are build on top of the protocol.

## Terminology

The following terms are used:

| Term      | Definition                                                    |
| --------- | ------------------------------------------------------------- |
| Packet    | A packet is a compleat message send over the network message. |
| Transport | The underlying transport protocol.                            |

## Layering

This protocol is set up to be layerd simulair to TCP/IP.
This is done to simplify the model and create a seperation of concerns.
The layers look like this, orderer from low to high:

| #   | Layer     |
| --- | --------- |
| 1   | Routing   |
| 0   | Transport |

## 0: Transmission

The transmission layer is responsible for transmitting packets beween two existing nodes.

Magic byte
Sequence
Permanent
type
receiver

Store-and-forward?

## ?????????

This section describes the format of packets to be send over the network.
It does not specify the format of the content of the packets, but the metadata of the packets.
This metadata is used in routing the packets around.

The the metadata part has a fixed length of `xxxx` bytes.
It contains the following parts:

- magic byte (4 byte, `0x20f57c03`)
- ttl (5 bit)
- start flag (1 bit)
- reserved (2 bit)
- communityid (2 byte)
- messageid (1 byte)
- sequence (1 byte)
- totalpackets (1 byte)
- data length (2 byte)
- signature (9 byte, SHA512withECDSA)

- magic byte (4 byte, `0x20f57c03`)
- data length (2 byte)
- ttl (5 bit)
- start flag (1 bit)
- evil flag (2 bit)
- reserved (1 bit)
- sequence (1 byte)

big endian
Evil bit?
SYN/ACK?
Checksum?

```
| 4 bytes    | 4 bits  | 4 bits |
+------------+---------+--------+
| Magic byte | Flags   | TTL    |
+------------+---------+--------+
```

# Magic byte

This magic byte is four bytes long, and fixed at `0x20f57c03`.
Any packet which don't start with this magic byte can safely be ignored.
It is added to makes sure you are dealing with an actual packet, instead of random noise.

## Flags

The first meaningfull part of a packet are the flags.
Flags are a single bit datatype where `1` equals `true` and `0` equals `false`.
These flags help with parsing the packet, as not all packet have the same format.
In total there are 4 flags, but not all of them are in use.
Flags are processed as they come in, so the left most flag is flag 0.

| Flag ID | Name                    |
| ------- | ----------------------- |
| 0       | End of packet           |
| 1       | Reserved for futher use |
| 2       | Reserved for futher use |
| 3       | Reserved for futher use |

### End of packet

This flag is `true` if this is the last packet in a single transmission.

## TTL

The TTL or time to live is an essential part of preventing flooding of the network.
Every message starts with a hop count between `1` and `15`.
At each hop the TTL counter is reduced by `1`.
A received packet should not be retransmitted if the TTL is `0` after substracting the counter.
It should still be processed like a normal packet.
