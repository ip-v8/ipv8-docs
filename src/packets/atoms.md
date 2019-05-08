# Atoms

## Integers

  Each common integer type can be an atom in an ipv8 packet. This includes the unsigned and signed form of an 8, 16, 32 and 64 bit integer.

  Each one of them will consume exactly as many bits in the sent packet as the size of the datatype without any overhead. (given that the pattern is known. See [Serialization](../payloads/serialization.md))

  All integers are sent and received in the same endianness which will be the Big Endian format.

## Floats

  Each common floating point data type (64 and 32 bits) can be sent in an ipv8 packet given that both the sender and receiver use the same floating point representation (IEEE754 float,double). This is important as both float and integer are transmitted in their binary form as unsigned integers.

## Characters

  A single ASCII character encoded in a single byte. TODO: not really an atom but an implementation detail where you can cast chars to u8 and back.

## Booleans

  A boolean can be sent with the overhead of 7 bits. Any nonzero 8 bit unsigned integer will be interpreted as True. Zero itself will be interpreted as False.

## Raw arrays

  Byte arrays can be sent with any conceivable content. The length must be known by the receiver (standardized per payload) as no length will be sent along with the data.

## Strings

  Raw array but cast to string. TODO: same as Characters.

## Variable length arrays

  Bytearrays of unknown length (by the receiver) can be sent like Raw arrays with as only the difference that the first block of the raw data will be the length of the raw data in bytes. The size of this blocks needs to be known by the receiver (standardized per payload). The size in bytes excludes the size of the length and thus is only the lenght of the raw data following.

## Flag bits

  A byte of flag bits can be sent. Each bit in the byte signifies a certain flag. In certain situations multiple bits together can form data of less than a byte in size when this is beneficial, to save some space. Flag bits are allways sent in multiples of one byte which implies that if less than 8 flag bits are sent the overhead will be the rest of the byte.

## Nested payloads

  A packet can comprise a nested payload, which means another packet is sent as part of the current packet. This other packet must be a [serializable payload](../payloads/serialization.md). Nested payloads are packed similar to variable length packets where the first **2** bytes form the length of the payload and the bytes after are the payload itself. Note that the length of a nested payload has a hard limit of 65536 (2^16) bytes.





