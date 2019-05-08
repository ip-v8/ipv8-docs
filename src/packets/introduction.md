
# Packets

An ipv8 packet consists of a list of any of the following building blocks which will from now on be called atoms. Each one of them will be described here.


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
