#### What are some of the problems with pricing rides by region?
> Small regions may lead to confusing pricing (the rider can walk 100 yards and see a very different price). Large regions hide price fluctuations between spaces like malls or airports. Mapping a coordinate to a region is efficient using data structures like quad-trees.

#### What data structure would be a good choice for storing locations and roads?
> A quadtree does not store the connection information between two locations. It assumes the distance between two points is Euclidean. This is incorrect for a road-connected map. A segment tree with points mapped to a Hilbert curve has the same problem. An adjacency matrix would require O(n^2) mappings for n points. An adjacency list requires O(n*neighbor) entries.

#### What is a good choice of protocol for sending location updates from drivers and riders?
>  A lightweight protocol written over UDP is a good choice for sending updates to the server. These messages do not need the ordering and acknowledgments that TCP provides.

#### What would be the best approach among the following to model a trip from pickup to drop off?
> The trip is an object that would have states and transitions like start -> run -> complete -> payment complete. Modeling it as a transaction would be incorrect. Modeling it as a graph traversal is unnecessary. The triproute can be shown to a user separately user history.
