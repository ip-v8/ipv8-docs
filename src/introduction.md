# IPv8 documentation

## Abstraction

This book is made to explain the protocol behind the IPv8 application and protocol.
The protocol has a few key features, namely:

- Unordered and connectionless, but reliable transmission
- Message authenticity
- Optional message encryption
- Low hop count
- No network flooding
- Protection against falsified node ID's
- Self repairing in case of node failure
- Almost guaranteed message delivery
- Protection agains malicious nodes
- Offline message delivery
- Route locality

## Layering

The protocol is set up in a layered fasion,
where every layer should be independent of the other.
This is done to simplify the model and create a seperation of concerns.
A simplified table is displayed below:

```
+---+-----------------+
| 5 | Community       |
+---+-----------------+
| 4 | Security        |
+---+-----------------+
| 3 | Routing         |
+---+-----------------+
| 2 | Verification    |
+---+-----------------+
| 1 | Transmission    |
+---+-----------------+
```

Every part will be explained separately in different chapters from low to high.
