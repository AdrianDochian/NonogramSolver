## Table of Contents

- **[About the game](#about_the_game)**
- **[State & Transition](#state_transition)**
- **[Solutions proposed](#solutions_proposed)**
    - [Depth First Search](#dfs)
    - [breadth First Search](#bfs)
    - [Iterative deepening Search](#ids)
    - [A* Search algorithm](#astar)
- **[Execution Result](#excution_result)**
    - [Input](#input)
    - [Output](#output)

## About the game

<a name="about_the_game"></a>

**Nonograms** are logic puzzles in which cells in a grid must be filled or left blank according to provided rows and
columns constraints

## State & Transition

<a name="state_transition"></a>

My game state is represented by a list pair objects defined with respect to a line
(row_index, list_of_possible_applications_for_next_constraint)<br>
Let's suppose we have a slate clean start of a 5x5 game <br>
<table>
  <tr>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
  </tr>
  <tr>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
  </tr>
  <tr>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
  </tr>
  <tr>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
  </tr>
  <tr>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
  </tr>
</table>

( with 1 2 constraints) on row with index 0 which means we have to place two continuous blocks <br>
of dimensions 1, respective 2, separated with at least one blank block<br>

A possible transition with respect to first line with index 0 is the answer to the question:<br>

- On what index can I place the first continuous block (which is 1) ?

1) It can start from 0
2) We must leave at least 1 empty block after it + (size_of_remaining_constraints - 1) +
   lengths_of_remaining_constraints <br>
   which for our case means 1 + (1 - 1) + 2 = 3 blocks
3) `1) + 2) =>` So that means we can place the block starting from {0, 1} columns
4) `1) + 2) + 3) =>`Same logic applies for remaining constraints on this line and for the other lines as well.

## Solutions proposed

<a name="solutions_proposed"></a>

<h7>The problem was treated as a state space search problem. </h7>

### Depth First Search

<a name="dfs"></a>

On each level of recursion for this approach `one` row constraint is abolished.<br>
Different paths of execution symbolize different orders of abolishing row constraints. <br>
The solution may be found only at the depth level equal to the number of row constraints. <br>
The solution is correct if when at the lowest depth level all column constraints are respected <br>

### Breadth First Search

<a name="bfs"></a>
This solution searches the logic `tree` one level at a time starting from the first. <br>
Due to the fact that the solution may only be found at the `leaf` level in the `tree` this solution is not
efficient. <br>

### Iterative deepening search

<a name="ids"></a>
This solution spawns recurrent depth first search executions with increasing level of depth. <br>
Again, due to the fact that the solution may only be found at the `leaf` level in the `tree`, this solution implies
much `overhead`. <br>
The (max_height - 1) iterations are destined to fail.

### A* Search algorithm

<a name="astar"></a>
This algorithm doesn't blindly try all the configurations. <br>
Based on the heuristic `f(game)` it decides if a certain state of the game has more chances to reach the solution. <br>
I do my state space search by abolishing row constraints but in the same time I am looking to respect consecutive column
constraints starting from first column. <br>
The `f(game)` score result (the lower the better) that a game state receives represents the number_of_columns -
the_number_of_columns_with_respected_constraints. <br>
Game states that can't be evolved in a solution are scored with +infinity.

## Execution Result

<a name="excution_result"></a>

## Input

<a name="input"></a>
Inputs (I use `testX.json` files) have the following format:

````
{
	"name": "music",
	"height": 10,
	"width": 10,
	"rows": [[4], [3, 1], [1, 3], [4, 1], [1, 1], [1, 3], [3, 4], [4, 4], [4, 2], [2]],
	"columns": [[2], [4], [4], [8], [1, 1], [1, 1], [1, 1, 2], [1, 1, 4], [1, 1, 4], [8]]
}
````

which will result in (I placed `||||` sequence instead of `1` character for visual effect):
<table>
  <tr>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
  </tr>
  <tr>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
  </tr>
  <tr>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
  </tr>
  <tr>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
  </tr>
  <tr>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
  </tr>
  <tr>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
  </tr>
  <tr>
    <th>0</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
  </tr>
  <tr>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
  </tr>
  <tr>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>0</th>
  </tr>
  <tr>
    <th>0</th>
    <th>|||||</th>
    <th>|||||</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
    <th>0</th>
  </tr>
</table>

## Output
<a name="output"></a>
After executing the notebook the `execution_result.json` output file will be generated:
It contains in json format an array of the following object structure:
````
{
    "name": "",
    "strategy": "",
    "nodes_generated": int,
    "nodes_expanded": int,
    "time": float,
    "solution": [[]]
}
````

A table overview of `execution_result.json` and my results would be:

<table>
  <tr>
    <th>Name</th>
    <th>strategy</th>
    <th>Nodes Generated</th>
    <th>Nodes Expanded</th>
    <th>Time(s)</th>
  </tr>
  <tr>
    <td>smile</td>
    <td>dfs</td>
    <td>51</td>
    <td>17</td>
    <td>0.0018548965454101562</td>
  </tr>
  <tr>
    <td>smile</td>
    <td>bfs</td>
    <td>25254</td>
    <td>13923</td>
    <td>2.493013620376587</td>
  </tr>
  <tr>
    <td>smile</td>
    <td>ids</td>
    <td>21137</td>
    <td>21110</td>
    <td>1.8002214431762695</td>
  </tr>
  <tr>
    <td>tower</td>
    <td>dfs</td>
    <td>174</td>
    <td>120</td>
    <td>0.010141611099243164</td>
  </tr>
  <tr>
    <td>tower</td>
    <td>bfs</td>
    <td>386341</td>
    <td>204976</td>
    <td>53.076340675354004</td>
  </tr>
  <tr>
    <td>tower</td>
    <td>ids</td>
    <td>309284</td>
    <td>309238</td>
    <td>29.666465282440186</td>
  </tr>
  <tr>
    <td>smile</td>
    <td>a_star</td>
    <td>22</td>
    <td>13</td>
    <td>0.0057811737060546875</td>
  </tr>
  <tr>
    <td>tower</td>
    <td>a_star</td>
    <td>22</td>
    <td>10</td>
    <td>0.007143259048461914</td>
  </tr>
  <tr>
    <td>music</td>
    <td>a_star</td>
    <td>2076</td>
    <td>1902</td>
    <td>13.899292469024658</td>
  </tr>
</table>
<hr>
