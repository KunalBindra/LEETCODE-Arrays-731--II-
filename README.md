# LEETCODE-Arrays-731--II-
Let's walk through a dry run of the `MyCalendarTwo` class, which is designed to allow booking events with the constraint that no triple bookings (three overlapping events) are allowed.

### Code Explanation:

- **Fields**:
  - `doublebookings`: Keeps track of time intervals where double bookings occur.
  - `overallbookings`: Keeps track of all bookings (single and double bookings).

- **Methods**:
  - `check(int s1, int e1, int s2, int e2)`: Returns true if two intervals (s1, e1) and (s2, e2) overlap.
  - `checkinterval(int s1, int e1, int s2, int e2)`: Returns the overlap of two intervals (s1, e1) and (s2, e2) as a new interval.
  - `book(int start, int end)`: 
    - First, it checks if the new booking would create a triple booking by checking against `doublebookings`. If yes, it returns `false` (booking not allowed).
    - Then, it checks for overlap with `overallbookings`. If there’s overlap, it records the overlap in `doublebookings`.
    - Finally, it adds the booking to `overallbookings`.

### Dry Run:

1. **First Call**: `book(10, 20)`
   - `doublebookings` is empty.
   - No overlap in `overallbookings`, so add the interval `[10, 20]` to `overallbookings`.
   - Return `true`.

   **State**:
   - `overallbookings = [[10, 20]]`
   - `doublebookings = []`

2. **Second Call**: `book(15, 25)`
   - `doublebookings` is empty.
   - There is overlap between `[10, 20]` and `[15, 25]`. The overlap interval `[15, 20]` is added to `doublebookings`.
   - Add the interval `[15, 25]` to `overallbookings`.
   - Return `true`.

   **State**:
   - `overallbookings = [[10, 20], [15, 25]]`
   - `doublebookings = [[15, 20]]`

3. **Third Call**: `book(20, 30)`
   - Check against `doublebookings` (no overlap with `[15, 20]`).
   - There is overlap between `[15, 25]` and `[20, 30]`. The overlap interval `[20, 25]` is added to `doublebookings`.
   - Add the interval `[20, 30]` to `overallbookings`.
   - Return `true`.

   **State**:
   - `overallbookings = [[10, 20], [15, 25], [20, 30]]`
   - `doublebookings = [[15, 20], [20, 25]]`

4. **Fourth Call**: `book(5, 15)`
   - Check against `doublebookings` (no overlap with `[15, 20]` or `[20, 25]`).
   - There is overlap between `[10, 20]` and `[5, 15]`. The overlap interval `[10, 15]` is added to `doublebookings`.
   - Add the interval `[5, 15]` to `overallbookings`.
   - Return `true`.

   **State**:
   - `overallbookings = [[10, 20], [15, 25], [20, 30], [5, 15]]`
   - `doublebookings = [[15, 20], [20, 25], [10, 15]]`

5. **Fifth Call**: `book(17, 22)`
   - Check against `doublebookings`:
     - Overlap found with `[15, 20]`, so triple booking would occur. 
     - Return `false`.

   **State** remains unchanged:
   - `overallbookings = [[10, 20], [15, 25], [20, 30], [5, 15]]`
   - `doublebookings = [[15, 20], [20, 25], [10, 15]]`

### Summary:

- The code prevents triple bookings effectively by tracking double overlaps and denying any new booking that would cause a third overlap.
