# Definition of Words

## Identity

A idendity is a collection of devices in the network.
Generally a identity maps one-to-one to a actual human.
Any device can create a identity, and invite a second device to the identity.
Devices with the same identity should always try to create a direct connection to eachother.

## Device

A device is a node inside of the network.
It has a identity attached to it, unless it's a beacon.

## Beacon

A beacon is a node with a fully open nat.
It is used as a way to accelerate bootstraping of known nodes.
If a identity indicates that it uses that beacon, al devices must try to connect to that beacon whenever possible.
Then if a device wants to find an identity it wil look up the beacons of this identity.
If a device of the identity is online it should be connected to one of the beacons.
