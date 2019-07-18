# Layering

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
