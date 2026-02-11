### Ride Matching
> We need a way to efficiently store and query nearby drivers. Let's explore different
> solutions we can incorporate into our design.
``` SELECT * FROM locations WHERE lat BETWEEN X-R AND X+R AND long BETWEEN Y-R AND Y+R ```

> We already have access to the latitude and longitude of our customers, and with
> databases like PostgreSQL and MySQL we can perform a query to find nearby driver
> locations given a latitude and longitude (X, Y) within a radius (R).
> SELECT * FROM locations WHERE lat BETWEEN X-R AND X+R AND long BETWEEN Y-R AND Y+R
> However, this is not scalable, and performing this query on large datasets will be
> quite slow.

### Geohashing
> Geohashing is a geocoding method used to encode geographic coordinates such as
> latitude and longitude into short alphanumeric strings. It was created by Gustavo
> Niemeyer in 2008.
> Geohash is a hierarchical spatial index that uses Base-32 alphabet encoding, the first
> character in a geohash identifies the initial location as one of the 32 cells. This cell
> will also contain 32 cells. This means that to represent a point, the world is
> recursively divided into smaller and smaller cells with each additional bit until the
> desired precision is attained. The precision factor also determines the size of the cell.

> For example, San Francisco with coordinates 37.7564, -122.4016 can be represented in geohash as 9q8yy9mf.
> Now, using the customer's geohash we can determine the nearest available driver by
> simply comparing it with the driver's geohash. For better performance, we will index
> and store the geohash of the driver in memory for faster retrieval.

### Quadtrees
> A Quadtree is a tree data structure in which each internal node has exactly four
> children. They are often used to partition a two-dimensional space by recursively
> subdividing it into four quadrants or regions. Each child or leaf node stores spatial
> information. Quadtrees are the two-dimensional analog of Octrees which are used to
> partition three-dimensional space.

> Quadtrees enable us to search points within a two-dimensional range efficiently,
> where those points are defined as latitude/longitude coordinates or as cartesian (x, y)
> coordinates.
> We can save further computation by only subdividing a node after a certain
> threshold.
> Quadtree seems perfect for our use case, we can update the Quadtree every time we
> receive a new location update from the driver. To reduce the load on the quadtree
> servers we can use an in-memory datastore such as Redis to cache the latest updates.
> And with the application of mapping algorithms such as the Hilbert curve, we can
> perform efficient range queries to find nearby drivers for the customer.
