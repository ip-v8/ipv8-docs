# Security

This system is designed to be secure.
It uses a DHT routing system under the hood, which historically has a lot of issues.
There are a few key points of security this is trying to solve.
These will be discussed in this page.

## Confidentiality

The system uses symmetric encryption to ensure confidentiality of the messages passed trough the network.
The key for this is shared during a handshake, if either of the two wants to set up a secured connetion.
This ensures complete confidentiality between two nodes.
More information about the implementation can be found on the [security](./layers/security/index.md) layer.

## Integrity

This ensures that the data has not been manipulated.
It is guaranteed by the [verification](./layers/verification/index.md) layer.
This page will go into more detail of the exact implementation,
but the more important

## Availability

This was the hardest problem to solve,
as there is no sure way to verify if a packet is intentionally dropped,
or that the node is not online.

A few of the implemented defenses:

- Difficult hashing of the public key to reduce the amount of new public keys.
- Periodic proof-of-work requests to limit the number of clients per node.
- Dropping of nodes with a high packet loss rate.

While these defenses don't prevent all attacks on the availability of the network,
it should reduce the amount and scale of most attacks.
You can find more information on the implementation on the [routing](./layers/routing/index.md) page.
