# tiny-chess-engine

A deterministic 4 KB chess engine in Python, entered in the make.fun tiny-chess-01 bounty.

main.py is the whole engine: an lzma-packed payload plus its unpacker, 4,064 bytes.
It plays through the trial env at MAKEFUN_ENV_URL (POST /game, POST /move).

## How it works

- 120-square board, pseudo-legal move generation, en passant and castling.
- Alpha-beta with null-window PVS, a transposition table, killer and history ordering,
  quiescence search with checks, null-move pruning, late move reductions, check extension.
- Evaluation: PeSTO piece-square tables blended for the middlegame plus the endgame king
  table, with material.

## Determinism

No clock and no unseeded randomness: every move comes from a fixed node budget, so a replay
plays the same game. The budget is 75,000 nodes a move for the first 700 moves, 37,500 after.
