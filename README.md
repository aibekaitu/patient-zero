# Assignment 4. Patient Zero

Student ID:253205
Name:Baimakhan Aibek
Group:SE-2512

This file is the report. Fill it in as you go. How to start: `START_HERE.md`. The task: `docs/Assignment4.pdf`.

## Program output

The 9 lines your program prints on your data (`java -cp out Main`):

    Mutations: 109
    Shared core: 1200
    Marker hits: 6
    First hit: 3829
    Border length: 3
    Shared words: 416
    Tests needed: 30
    Cheapest testing: 122
    Longest chain: 26

My outbreak report (a screenshot of `output/outbreak.html`):

![outbreak](output/outbreak.png)

## Questions

Answer in your own words, two or three sentences each.

### Mission 1 — Edit Distance

The cell d[i][j] shows the minimum number of operations needed to transform the first i characters of A into the first j characters of B. It is calculated using insertion, deletion, and replacement, choosing the minimum cost.

### Mission 2 — Longest Common Subsequence

A subsequence can skip characters while keeping their order, but a substring must contain consecutive characters. My Shared core can be larger because LCS allows matching characters at different positions.

### Mission 3 — Prefix Function and KMP

The prefix function shows the length of the longest matching proper prefix and suffix. KMP uses this information to avoid checking characters again, so the text pointer never moves backward. My marker is GGAGCAGGA and its Border length is 3 because GGA appears at both the beginning and the end.

### Mission 4 — Rabin-Karp

We must compare characters because different strings can have the same hash value. If many windows have the same hash, the algorithm becomes slower because it needs more character comparisons.

### Mission 5 — Tree DP

Each person has two states: tested and not tested. If a person is not tested, all their children must be tested; otherwise we choose the cheaper state for each child. A greedy approach may fail because it does not consider testing costs and the entire tree structure.
## AI use

**AI use:** ## I used ChatGPT to understand the assignment and check errors.

## Timing (Mission 7)

Milliseconds, average of 3 runs, from `java -cp out Bench`.

| Test | Size | Time |
|---|---|---|
| Naive search | 20 000 | 40.0 ms |
| Naive search | 40 000 | 91.5 ms |
| Naive search | 80 000 | 211.8 ms |
| KMP | 20 000 | 4.6 ms |
| KMP | 40 000 | 2.2 ms |
| KMP | 80 000 | 0.7 ms |
| Edit distance | 500 | 9.7 ms |
| Edit distance | 1000 | 13.0 ms |
| Edit distance | 2000 | 29.3 ms |
| Edit distance | 4000 | 109.2 ms |

### Analysis

Naive search becomes about 2.3 times slower when the text size doubles. KMP has linear time complexity, but its measured times decreased, likely due to JVM warm-up and measurement effects. Edit distance grows approximately quadratically for large inputs, approaching four times the runtime when both string lengths double.

What do the numbers say about how the time grows? When you double the size, by how much does each time grow? Two or three sentences.

## Complexity

n is the length of the text (or of a strain), m the length of the pattern, k the length of the window, v the number of people. Fill in every algorithm you wrote.

| Algorithm | Time | Space | Assumptions |
|---|---|---|---|
| Edit distance | O(n*m) | O(n*m) | Two-dimensional DP table |
| LCS | O(n*m) | O(n*m) | Two-dimensional DP table |
| Prefix function and KMP | O(n+p+h) | O(p+h) | p = marker length, h = number of matches |
| Rabin-Karp (shared words) | Expected O(n+m+c*k), worst O(n*m*k) | O(m) | c = number of hash-match candidates; worst case has many collisions |
| Tree DP | O(v) | O(v) | Each person and infection link is processed once |
## Before you submit

- The four files in `data` and the screenshot `output/outbreak.png` are in the repository.
- `java tools/Check.java` shows all examples right.
- This README is filled in, the program output and the section AI use included.
- The work is pushed to main (at least one commit per mission) and the repository is public.
- The link is attached in Moodle.
