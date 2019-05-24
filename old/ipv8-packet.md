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

## Verify (OpenSSL)
1. Get the Public key from the BinKey payload
2. Parse it into a proper key (add pem header/trailer and give to to openssl)
3. Find out its algorithm and curve
4. Use the algo/curve to determine the length of the signature
5. Extract the ECDSA signature to `r`,`s`
6. Parse `r`,`s` into an `EcdsaSig`
7. Verify the signature with the public key

## Verify (libnacl-ed25519)
1. Get the public key from the BinKey payload (detectable by the `libnacl` prefix)
2. Parse into ed25519 public key
3. extract the signature from the end (length is known)
4. Verify the signature with the key

## The rest
The rest is handled by the correct community

(No communities exist in our implmentation yet)


# Serializing a packet

## Header
//TODO: Implement

## Signing (OpenSSL)
1. Get the private key from the user.
2. Use the algorithm and corresponding curve of the key to calculate the signature (r,s) and needed padding.
3. Return a Signature

## Signing (libnacl-ed25519)
1. Use the users private key to generate a signature over the given packet.
2. Append the signature.

