### Ref  : [게임 이론의 미니맥스 알고리즘 | 세트 1(소개) - GeeksforGeeks](https://www.geeksforgeeks.org/minimax-algorithm-in-game-theory-set-1-introduction/)

## Minimax Value
- Given a game tree, the optimal strategy can be determined by working out the <font color="#fac08f">minimax value</font> of each state in the tree, which we write as <font color="#fac08f">$MINIMAX(s)$</font>.
	- The minimax value is the utility of being in that state, <font color="#fac08f">assuming that both players play optimally</font> from there to the end of the game.
	- The minimax value of a terminal state is just its utlity.
	- In a non-terminal state, MAX prefers to move to a state of maximum value when it is MAX’s turn to move, and MIN prefers a state of minimum value.
	- Therefor, $$MINIMAX(s) =\begin{cases}UTILITY(s) &\text{if } TERMINAL(s)\\ max_{a\in ACTIONS(s)}MINIMAX(RESULT(s,a)) &\text{if }PLAYER(s) = MAX\\ min_{a\in ACTIONS(s)}MINIMAX(RESULT(s,a)) &\text{if }PLAYER(s) = MIN \end{cases}$$

## Code
> Finds the best move (for MAX) by trying all actions and choosing hte one whose resulting state has the highest $MINIMAX$ value.
```pseudo code
function MINIMAX-SEARCH(game,state) returns an action
	plyer <- game.TO-MOVE(state)
	value, move <- MAX-VALUE(game,state)
	return move

function MAX-VALUE(game,state) returns a (utility,move) pair
	if games.IS-TERMINAL(state) then return game.UTILITY(state,player), null
	v, move <- -∞
	for each a in game.ACTIONS(state) do
		v2,a2 <- MIN-VALUE(game,game.RESULT(state,a))
		if v2 > v then
			v,move <- v2, a
	return v,move

function MIN-VALUE(game,state) returns a (utility,move) pair
	if games.IS-TERMINAL(state) then return game.UTILITY(state,player), null
	v, move <- ∞
	for each a in game.ACTIONS(state) do
		v2,a2 <- MAX-VALUE(game,game.RESULT(state,a))
		if v2 < v then
			v,move <- v2, a
	return v,move
```

## Performance
- \# of game states is exponential in the depth of the tree
	- We should cut(pruning)
- The particular technique we examine is called alpha-beta pruning

## Alpha-Beta search algorithms
- The general principle
	- Consider a node somewhere in the tree, such that Player has a choice of moving to .
	- If Player has a better choice either at the same level ($m^′$) or ay any point higher up in the tree($m$), then Player will never move to .
	- So once we have found out enough about (by examining some of its descendants) toreach this conclusion, we can prune it.
- $$\begin{align}\alpha &=\text{the value of the best (i.e.,highest-value) choice we have found so far at any choice point along the path for MAX }\\&=\text{"at least"}\\\beta &=\text{the value of the best (i.e.,highest-value) choice we have found so far at any choice point along the path for MIN }\\&=\text{"at most"}\end{align}$$
### Code
```pseudo code
function ALPHA-BETA-SEARCH(game,state) returns an action
	plyer <- game.TO-MOVE(state)
	value, move <- MAX-VALUE(game,state,-∞,∞)
	return move

function MAX-VALUE(game,state,α,β) returns a (utility,move) pair
	if games.IS-TERMINAL(state) then return game.UTILITY(state,player), null
	v, move <- -∞
	for each a in game.ACTIONS(state) do
		v2,a2 <- MIN-VALUE(game,game.RESULT(state,a),α,β)
		if v2 > v then
			v,move <- v2, a
			α <- MAX(α,v)
		if v >= β then return v,move
	return v,move

function MIN-VALUE(game,state,α,β) returns a (utility,move) pair
	if games.IS-TERMINAL(state) then return game.UTILITY(state,player), null
	v, move <- ∞
	for each a in game.ACTIONS(state) do
		v2,a2 <- MAX-VALUE(game,game.RESULT(state,a),α,β)
		if v2 < v then
			v,move <- v2, a
			β <- MIN(β,v)
		if v <= α then return v,move
	return v,move
```


## Further Study
- Monte Carlo Tree Search
- reinforcement learning
- book : Reinforcement Learning: An Introduction (Richard S. Sutton and Andrew G. Barto)
- video : Reinforcement Learning Lecture Series 2021 (DeepMind X UCL)