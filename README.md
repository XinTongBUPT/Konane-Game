# Konane-Game
A compelete Konane game using minimax and alpha-beta pruning.
## What I did

I'll be implementing minimax and alpha-beta pruning for an agent playing one such game—that of
konane. 
I finished my implementing one player using Minimax and another player using Alpha-Beta Pruning.

Run the following from your terminal:
```bash
python main.py $P1 $P2
```

By default, `main.py` will setup a human player versus a random player on a board that is 10x10. During **Human** mode, move the cursor with the ARROW keys and select the tile with SPACE. When it is a computer's turn, advance the game with the SPACE key. To see the game board in your terminal, you need a minimum terminal size of (rows + 2) x (columns + 2) to see the whole board. To exit the game, kill the process in your terminal (e.g., with CTRL-c).

You can change the game settings by passing in values to `python main.py`. You need to pass in _exactly_ two arguments. Valid arguments are as follows:

* H (Human)—manually select the tile to move and to where you will move it. Legal moves will be executed.
* D (Deterministic)—the agent will select the first move that it finds (the leftmost option in the tree) during its 
traversal.
* R (Random)—the agent will pick a random move.
* M (Minimax)—the agent will pick a move using the minimax algorithm. You will be prompted for a max. search depth.
* A (Alpha-beta pruning)—the agent will pick a move using AB pruning. You will be prompted for a max. search depth.

Passing in an invalid number or type of arguments will result in the system defaulting to a human vs a random player.

## Introduction: Konane

Also known as Hawaiian checkers, [konane](https://en.wikipedia.org/wiki/Konane) is a strategy game played between two
players. Players alternate taking turns, capturing their opponent's pieces by jumping their own pieces over them (if 
you're familiar with checkers, there is a strong structural analogy to be made here). The first player to be unable to
capture any of their opponent's pieces loses.

The full rules can be read *[here](https://en.wikipedia.org/wiki/Konane#Rules_and_gameplay)* or
*[here](http://www.konanebrothers.com/How-to-Play.html)*. Here's my (rather terse) version, though:


![Konane Board](pictures/board.jpg "Board")

1. Black typically starts. They take one of their pieces off of the board.

![Konane Board](pictures/initial.jpg "Board")

2. White then takes one of their pieces off of the board from a space _orthogonally_ adjacent to the piece that black
removed.

![Konane Board](pictures/jump.jpg "Board")

3. Each player then alternately moves their pieces in capturing moves. A capturing move has a stone move in an
orthogonal direction, hopping over an opponent's piece. Multiple captures may be made in a turn, as long as the stone
moves in the same direction and captures at least one piece.

![Konane Board](pictures/nomoves.jpg "Board")

4. The first player to be unable to capture a piece loses. :(

## Play the game

You'll be implementing minimax and alpha-beta pruning for an agent playing one such game—that of
konane. But first, you should get familiar with how the game is played. To do this, play the game with the provided code. You've been distributed a codebase which includes an interface for playing the game in a variety of modes.
Notably, you don't need to actually _make_ the game of konane—just to make an agent that plays it.

Run the following from your terminal:
```bash
python main.py $P1 $P2
```

By default, `main.py` will setup a human player versus a random player on a board that is 10x10. During **Human** mode, move the cursor with the ARROW keys and select the tile with SPACE. When it is a computer's turn, advance the game with the SPACE key. To see the game board in your terminal, you need a minimum terminal size of (rows + 2) x (columns + 2) to see the whole board. To exit the game, kill the process in your terminal (e.g., with CTRL-c).

You can change the game settings by passing in values to `python main.py`. You need to pass in _exactly_ two arguments. Valid arguments are as follows:

* H (Human)—manually select the tile to move and to where you will move it. Legal moves will be executed.
* D (Deterministic)—the agent will select the first move that it finds (the leftmost option in the tree) during its 
traversal.
* R (Random)—the agent will pick a random move.
* M (Minimax)—the agent will pick a move using the minimax algorithm. You will be prompted for a max. search depth.
* A (Alpha-beta pruning)—the agent will pick a move using AB pruning. You will be prompted for a max. search depth.

Passing in an invalid number or type of arguments will result in the system defaulting to a human vs a random player.


### Part 1: Minimax

Minimax is an algorithm for determing the best move in an adverserial game. Its objective is to find the move that 
_maximizes_ the gain for the player while _minimizing_ their loss. Since "maximin" sounds kind of dumb, we get 
"minimax." Minimax is typically employed in competitive, discrete- and finite-space games with abstracted time and 
perfect information.

I completed the implementation of `MinimaxPlayer` in `player.py`. In your implementation, you need to be aware of 2 things: the max depth and the evaluation function.  The max depth is provided to the constructor of the `MinimaxPlayer` and defines the maximum number of plies that the player will simulate when choosing a move.  The evaluation function defines a score for a terminal node in the search.  Use the function `h1` defined in the parent class `Player` as your evaluation function.

### Part 2: Alpha-Beta Pruning

I noticed that minimax starts to get terribly slow when I set maximum search depth to values above, say, 4.
For comparatively "bushy" games (e.g., _chess_, _go_, etc.) the branching
factor is prohibitively large, which is why agents that play these games use cleverer algorithms to choose what move to
take next.

One such cleverer algorithm (although still not clever enough to do well at games like _GO_) is a modification of
minimax known as _alpha-beta pruning_. They are, at their core, the _same algorithm_. The distinction is that AB pruning
_ignores_ subtrees that are provably worse than any that it has considered so far. This drastically reduces the runtime
of the algorithm.\* Since AB pruning is a variant on minimax, I'm not really writing a new algorithm; rather, I'm
taking your implementation of minimax and making it a little smarter.

\* Strictly speaking, it doesn't change the upper bound on the algorithm's runtime, since in the worst-case one must
still search the entire tree. In practice, however, the performance difference is very noticeable.

## Notes

* `player.py`—this is the file with player class.
* `main.py`—to play the game (in Human mode) or to watch your agents duke it out, run `python main.py`. Use the arrow 
keys and the spacebar to select your actions.
* `test.py`—run tests with `python test.py`.
* `game_manager.py`—holds the board representation and handles turn-taking.
* `game_rules.py`—code determining available moves/their legality, etc.
* You can change the type of player, the board size, etc. in `main.py`
