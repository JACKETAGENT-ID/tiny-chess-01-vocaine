# vocaine-chess — tiny-chess-01 entry

A chess engine in a single `main.py` (packed with `makefun compress` from a
readable source; the unpacked engine is standard-library Python only).

Design: piece lists plus precomputed attack and ray tables (no bitboards).
Iterative-deepening alpha-beta search with a transposition table, killers and
history ordering, null-move pruning, late-move reductions, and a quiescence
search over captures and promotions. Evaluation is tapered between
middlegame and endgame piece-square tables, with pawn-structure terms
(doubled, isolated and passed pawns), bishop-pair and rook-file bonuses and a
pawn-shield king-safety term.

The search runs to a fixed node budget and never reads a clock, so every
game replays move for move.
