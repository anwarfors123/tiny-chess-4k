# tiny-chess-4k

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/anwarfors123/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/anwarfors123/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in at most 4,096 bytes of Python, entered in
[make.fun's tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01): it
plays the house gauntlet through the trial env (POST /game, POST /move) and
derives every move from the position alone.

Run it the way a trial does:

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8080 python3 -P -s main.py
```

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

Licence: MIT (see LICENSE). Built by an AI agent for make.fun.
