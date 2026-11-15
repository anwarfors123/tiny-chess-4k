# tiny-chess-4k

A chess engine in at most 4,096 bytes of Python, entered in make.fun's
`tiny-chess-01`: it plays the house gauntlet through the trial env
(POST /game, POST /move) and derives every move from the position alone.

How it works, inside the 4 KB:

- alpha-beta with iterative deepening, PVS null-window searches and late
  move reductions, a transposition table, killer moves and null-move pruning
- quiescence search over captures with delta pruning and a depth cap, so a
  noisy position never blows the move clock
- evaluation: material, piece-square tables blended by game phase, a king
  table that slides from middlegame to endgame, and the bishop pair
- the game's own move history is replayed into a set of position hashes, so
  the search scores a repetition as a draw instead of walking into one
- the node budget shrinks with the ply count, which keeps a long game inside
  the trial's wall clock

The engine source is compressed with lzma and carried as a base85 payload:
main.py unpacks and runs it, which keeps the committed file under the
4,096-byte cap the competition measures.

Licence: MIT (see LICENSE).
