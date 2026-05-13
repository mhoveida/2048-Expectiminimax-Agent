This project implements an **Intelligent Agent** designed to play the game **2048** using advanced search algorithms and heuristic evaluations.

### Core Architecture: Expectiminimax

The decision-making process of the `IntelligentAgent` is driven by the **Expectiminimax** algorithm. This is an extension of the Minimax algorithm used in games with an element of chance (like 2048, where new tiles are spawned randomly).

* **Player Turn (MAX)**: The agent tries to maximize its utility by choosing the move that leads to the best future grid state.
* **Computer Turn (CHANCE)**: Instead of a simple "Min" player, the agent calculates an **expected value** based on the probability of the computer placing a '2' tile (90%) or a '4' tile (10%) in available cells.
* **Alpha-Beta Pruning**: The algorithm uses Alpha-Beta pruning to discard branches in the search tree that cannot possibly influence the final decision, significantly improving performance.
* **Iterative Deepening**: The agent uses a `while True` loop to search deeper into the game tree as long as it is within the `time_limit` (0.18 seconds).

---

### Heuristic Evaluation

Since the agent cannot search until the end of the game, it uses an `evaluate` function to score the quality of a grid state. The final score is a weighted sum of several factors:

| Heuristic | Description | Weight |
| --- | --- | --- |
| **Empty Tiles** | Encourages keeping more empty spaces on the board. | 1 |
| **Max Tile** | Rewards the agent for reaching higher tile values (e.g., 2048). | 75 |
| **Monotonicity** | Checks if tile values strictly increase or decrease along rows and columns, keeping large tiles in corners. | 7.5 |
| **Smoothness** | Minimizes the value difference between adjacent tiles to make merging easier. | 0.75 |
| **Merge Potential** | Rewards states where adjacent tiles have the same value. | 1.25 |
| **Weighted Tile** | Uses a gradient weight matrix to push the largest tiles toward a specific corner. | 100 |

---

### Project Structure

The repository is organized into several functional components:

* **`GameManager.py`**: The main engine that handles turns between the Player and Computer, manages the time limit, and detects game over states.
* **`Grid.py`**: Handles the internal 2D array representation, tile merging logic, and available move detection.
* **`ComputerAI.py`**: Implements the "adversary" which simply places tiles in random empty cells.
* **`Displayer.py`**: Provides a color-coded terminal interface to visualize the game in real-time.
* **`Heuristics.py`**: A utility script used to run automated experiments and find the optimal weights for the evaluation function.

### Requirements

* **Python 3**
* **NumPy**
