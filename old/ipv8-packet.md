# IPv8 Packet

## Overview
| version number | master_peer.mid |    msg_id    |  payloads  |   trailer  |
|----------------|-----------------|--------------|------------|------------|
|    2 bytes     |    40 Bytes     |    1 byte    |   x bytes  |   x bytes  |


### Version number
* 1: Dispersy
* 2: py-ipv8

### Master Peer Mid
SHA1 hash of the public key

### Message ID
A message ID which determines which community and of what type the message is.

Basically to determine to whom to pass the decoded packet.

### Payloads
The first


### Trailer
The trailer almost always consist of a signature signing the packet

# Deserializing a packet
1. Header
2. Verify
3. Rest

## Header
//TODO: Implement

## Verify
1. Get the Public key from the BinKey payload
2. Parse it into a proper key (add pem header/trailer and give to to openssl)
3. Find out its algorithm and curve
4. Use the algo/curve to determine the length of the signature
5. Extract the signature to `r`,`s`
6. Parse `r`,`s` into a `EcdsaSig`
7. Verify the signature with the public key

## The rest
The rest is handled by the correct community

(No communities exist yet)


# Serializing a packet

## Header
//TODO: Implement

## Signing

