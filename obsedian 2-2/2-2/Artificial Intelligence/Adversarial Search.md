## Reference : [Adversarial Search Algorithms in Artificial Intelligence (AI) - GeeksforGeeks](https://www.geeksforgeeks.org/adversarial-search-algorithms/)
## Base
- Competitive environments
	- Two or more agents have conflicting goals, giving rise to <font color="#fac08f">adversarial search</font> problems.
- We focus on games:
	- Such as tic-tac-toe, chess, Go, and poker.
	- For AI researchers, the simplified nature of these games is a plus.
	- The state of a game is easy to represent.
	- Agents are usaully resctricted to a small number of actions whose effects are defined by precise rules.
- We explicitly model adversarial agents with the techniques of <font color="#fac08f">adversarial game-tree search</font>

## Two-Player Zero-Sum Games
- The games most commonly studied within AI (e.g., chess and Go) are what game theorists call <font color="#fac08f">deterministic, two-player, turn-taking, perfect information, zero-sum games</font>.
	- **“Perpect information”** is a synonym for **“fully observable”**.
	- **“Zero-sum”** means that what is good for one player is just as bad for the other
		- There is no win-win outcome.
	- For games, we often use the term **move** as a synonym for **“action”** and **position** as a synonym for **“state”**.
- Specification
	- In our game, we call our two players <font color="#fac08f">MAX</font> and <font color="#fac08f">MIN</font>.
	- MAX moves first, and then the players take turns moving until the game is over.
	- At the end of the game, points are awarded to the winning player and penalties are given to the loser.
- A game can be formally defined with the following elements:
	- $S_0$: The **initial state**, which specifies how the game is set up at the start.
	- $TO−MOVE(s)$ (or $PLAYER(s)$): The player whose turn it is to move in state $s$.
	- $ACTIONS(s$)$: The set of legal moves in state $s$.
	- $RESULT(s,a)$: The **transition model**, which define the state resulting from taking action in state .
	- $IS−TERMINAL(s)$ (or simply $TERMINAL(s)$): A **terminal test**, which is true when the game is over and fasle otherwise. States where the game has ended are called **terminal states**.
	- $UTILITY(s,p)$ (or $UTILITY(s)$): A **utility function** which defines the final numeric value to player when the game ends in terminal state $s$.

## Algorithms 
- #### [[Minimax search]]