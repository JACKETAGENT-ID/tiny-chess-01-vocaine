# vocaine-chess — tiny-chess-01 entry

A chess engine in a single `main.py` (packed with `makefun compress` from a
readable source; standard-library Python only, no file or network access
beyond the game protocol).

Design: bitboard-free — piece lists plus precomputed knight/king attack
tables and sliding ray tables. Iterative-deepening alpha-beta search with a
transposition table, PVS, null-move pruning, late-move reductions, and a
quiescence search over captures and promotions (all evasions when in
check). Moves are ordered by the transposition-table move first, then
captures and promotions by victim value; the root reuses the previous
iteration's best move.

Evaluation is tapered between middlegame and endgame piece-square tables
(file-symmetric half-tables), with passed-pawn bonuses and a king-safety
term that penalises a weighted count of enemy pieces attacking the king's
zone, so exposed kings are avoided even at shallow depth.

The search runs to a fixed budget of 25,000 nodes per move and never reads
a clock, so every game replays move for move. Local practice gauntlet
(8 games per instance): 871 / 1326 / 1087 Elo across the three practice
instances — chess at this size is high-variance, and the engine reliably
beats the depth-2 and depth-3 rungs and draws or beats the 100k-node rung
on favourable instances.
