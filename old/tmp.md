# Deserializing a packet

1. Header
2. Verify
3. Rest


## Header
The header consists of

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
