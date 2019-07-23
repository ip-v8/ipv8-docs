# Trust

Trust in a distributed network has been proven to be a difficult challenge.
structured p2p networks like DHT's use a high level of trust,
making them vulnerable to a range of attacks.
Distnet tries to defend against these attacks by using a routing algorithm derrived from SPROUT and Pastry.
It uses a web of trust defined by the overlay to create a routing table for that overlay.
While there is a global network spanning all nodes which can be used as a fallback,
the routing table for that overlay is used till the node cannot forward the message any better.
When that happens the global network takes care of the last mile using tratitional Pastery.

In this network trust is defined by a number between -1 and 1 (inclusive).
Every node starts of with a neutral trust of 0.
An overlay can use it's own algorithm to register a new trust value for a node.
For example a social network can use the trust value to indicate the relationship between two identities.
If two identities have a close relation the overlay might set the trust to 0.9,
but if they barely know each other it might give a rating of 0.2.
A negative rating is also possible,
if this is given the node tries to avoid this node,
and never connects to it directly.

## Building the trust graph

The trust of a node is stored in the Trustchain,
of which the starting node has a local copy of from the last time it connected to the network.
It will use this to build the trust graphs of all of the overlays as well as an aggregated one, which combines all the overlays into one.
This aggregated one is used when creating the globally linked network.

When building the trust graph for a overlay it first reads out all ratings given to nodes.
Negative ratings are ignored here.
If the rating is higher than a treshhold (let's say 0.6),
then the process is repeated but for that node.
So it reads out the trustchain for that node,
and get's the trust.
That trust is multiplied by the trust of the origional node,
giving the relative trust of the new node.
This is then added to the list of nodes.

A quick example:

```
Node A tries to connect to the network.
It finds node B in it's trust graph, with a trust rating of `0.7`.
Node A explores the Trustchain of node B, finding a new node C with a rating of 0.4.
The ratings of node B and C are multiplied, giving the relative rating of 0.28 for C from A.
If node C already existed in the graph of node A then the trusts are added together.
So if node A had a trust of 0.3 for node C, then the new trust will be 0.58.
```

To build the aggregated graph it simply combines all graphs,
with adding the different trusts together.
If a collision occures the trust values are added together,
giving that node a higher incentive to be connected to.

## Building the routing table

When a node starts up it will connect to a boostrap node and do the boostrapping procedure as notmal with Pastery.
In the procedure it tries to connect to a few of the most trusted nodes as defined in the trust graph.
This is used to build the routing table.
While the is going on it tries to swap out any random nodes with nodes with a higher trust rating.
This would create
