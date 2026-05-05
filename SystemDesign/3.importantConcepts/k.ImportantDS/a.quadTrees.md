### A Quad Tree is a tree data structure that divides a 2D space into four equal parts recursively until each region becomes simple enough to manage.
#### What is a Quad Tree?
- Imagine you have a big square land.
- If there are too many things inside that land (like houses, trees, enemies in a game), it becomes hard to manage.
- So what do we do?
- 👉 We divide the square into 4 smaller squares.
- Each smaller square can again be divided into 4 more squares, and so on.
- This recursive 4-way division is called a Quad Tree.

### Problem: Find Nearby Stores
- Suppose:
- City has 1,00,000 stores
- User opens app and searches:
  - 👉 “Find stores within 2 km”
- Without Quad Tree:
  - You check distance with all 1,00,000 stores
  - That’s slow ❌
- How Quad Tree Solves This:

#### Step 1️⃣: Divide the City Map
- The entire city map is treated like a big square.
- Quad Tree divides it into 4 parts:

+--------------------+
| Q1 | Q2            |
|----+---------------|
| Q3 | Q4            |
+--------------------+
- If one region has too many stores → divide again.
- Only dense areas are split further.

#### Step 2️⃣: Store Each Shop in Its Region
- Each store is saved inside a specific quadrant based on its coordinates (latitude & longitude).
- Example:
  - Store A → Q1
  - Store B → Q3
  - Store C → Q3 → sub-quadrant
  - So now stores are grouped by location.
- Step 3️⃣: User Location Query
  - User is at (x, y).
  - We create a search square or circle around the user (2 km radius).
- Instead of checking all stores:
  - ✔ We check only quadrants that overlap with that circle
  - ❌ Ignore far-away quadrants completely
