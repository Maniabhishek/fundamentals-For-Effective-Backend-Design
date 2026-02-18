### Two important concepts when finding nearby business or stores

### GeoHash
- Reduce the two-dimensional longitude and latitude data into a one-dimensional string of letters and digits.
- Recursively Divide the world into smaller and smaller grids with each additional bit.
- The longer a shared prefix is between two geohashes, the closer they are.

<img width="464" height="314" alt="image" src="https://github.com/user-attachments/assets/84542c12-02aa-4bb0-97c8-d73eb812287d" />
- Cons
  - Have boundary issues:
  - Two locations can be very close but have no shared prefix at all.
  - Two locations can have a long shared prefix, but they belong to different geohashes.

### Quadtree
- Partition a two-dimensional space by recursively subdividing it into four quadrants (grids) until the contents of the grids meet certain criteria.
- Quadtree is an in-memory data structure and it is not a database solution.
