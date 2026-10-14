# SLE-4
# Tic-Tac-Toe Search Agent: Minimax vs Alpha-Beta Pruning

* **Course**: 02AML204 – Introduction to Artificial Intelligence[span_1](start_span)[span_1](end_span)
* **Student Name**: Nikesh Rathod[span_2](start_span)[span_2](end_span)
* **PRN**: 25UAM099[span_3](start_span)[span_3](end_span)
* **Division**: B[span_4](start_span)[span_4](end_span)
* **GitHub / Portfolio**: [rnikesh7218-maker](https://github.com/rnikesh7218-maker)[span_5](start_span)[span_5](end_span)

---

## Architecture Decision Record (ADR)

* **Title**: Use Minimax with Alpha-Beta Pruning as the main solver of my Tic-Tac-Toe Search Agent, instead of plain Minimax[span_6](start_span)[span_6](end_span)
* **Status**: Accepted[span_7](start_span)[span_7](end_span)

### 1. Context
The system is a Tic-Tac-Toe search agent where X is to move, finding the best result under perfect play (+1 = X wins, 0 = draw, -1 = O wins)[span_8](start_span)[span_8](end_span). Plain Minimax was profiled against Minimax with Alpha-Beta Pruning across best, average, and worst-case boards[span_9](start_span)[span_9](end_span).

### 2. Decision
* **Chosen Solver**: Minimax with Alpha-Beta Pruning[span_10](start_span)[span_10](end_span).
* **Baseline**: Plain Minimax is retained in the project to verify that Alpha-Beta produces identical results[span_11](start_span)[span_11](end_span).
* Both engines share the same Game Rules Module (`winner` and `get_moves`), use the same move order (cells 0 to 8), and return a `(value, nodes)` pair[span_12](start_span)[span_12](end_span).

### 3. Alternatives Considered
* **Alternative 1 – Plain Minimax**: Kept as a correct, simple baseline, though it visits every position (e.g., 549,946 on an empty board)[span_13](start_span)[span_13](end_span).
* **Alternative 2 – Alpha-Beta with move ordering**: Could prune further, but not built or tested yet[span_14](start_span)[span_14](end_span).
* **Alternative 3 – Depth-limited Minimax with evaluation**: Necessary for larger games like Chess, but Tic-Tac-Toe is small enough to search completely[span_15](start_span)[span_15](end_span).

### 4. Performance & Rationale
* **Worst-case (Empty board)**: Minimax took 648.3 ms (549,946 nodes), while Alpha-Beta took 24.9 ms (18,297 nodes)—about 30x fewer positions and 96.7% less work[span_16](start_span)[span_16](end_span).
* **Average-case (5 empty cells)**: Alpha-Beta searched 93 nodes (0.1433 ms) compared to Minimax's 238 nodes (0.3148 ms)[span_17](start_span)[span_17](end_span).
* **Best-case (3 empty cells)**: Performance was practically identical; Alpha-Beta was marginally slower (0.0189 ms vs 0.0177 ms) due to overhead when very little pruning is possible[span_18](start_span)[span_18](end_span).

### 5. Consequences
* **Positive**: Same correct outputs with significantly fewer node expansions on large boards, easy to test, and modular design allows future upgrades[span_19](start_span)[span_19](end_span).
* **Negative / Trade-offs**: Slightly more complex code logic; pruning depends entirely on a fixed move order; Tic-Tac-Toe's small size does not prove scalability to larger games like Chess[span_20](start_span)[span_20](end_span).

---

## AI Contribution Note
* **AI Tools Used**: Claude (Anthropic)[span_21](start_span)[span_21](end_span).
* **AI Assistance**: Explained the ADR format, helped draft the Minimax/Alpha-Beta and profiling code in SLE-2, and assisted in formatting the Word document[span_22](start_span)[span_22](end_span).
* **Student Contribution**: Chosen the algorithms, evaluated results and the C4 model, verified data accuracy, and prepared for the viva defense[span_23](start_span)[span_23](end_span).
*
