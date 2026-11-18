# TinyChess4K

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Rifai20388/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Rifai20388/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 4 KB of Python, built for make.fun's **tiny-chess-01**
bounty ("Build the strongest chess engine in 4 KB of Python", $500 in USDC).

`main.py` is the whole engine: a 0x88 board, alpha-beta with iterative
deepening to a fixed node budget, quiescence over captures, promotions and
replies to a check, a transposition table, MVV-LVA captures, killer moves
and a history heuristic, and an evaluation of material, piece-square
tables and the bishop pair. It plays the house gauntlet through the env
(`POST /game`, `/move`, `/resign`) and never calls a model.

The search runs to a fixed number of nodes per move, never a clock, and
uses no unseeded randomness, so a trial's replay plays the same games
move for move. `src/engine.py` is the readable source the compressed
`main.py` is packed from.

## The size rule

- `main.py` is at most 4,096 bytes as committed (the kit's `makefun
  compress` packs `src/engine.py` into it with LZMA).
- The whole snapshot (this README, LICENSE, `main.py` and the claim
  file) is at most 8,192 bytes, no file over 4,096. MIT licence.

## Grade it locally

From the kit directory, with the repository as the bot:

    node cli/makefun.mjs grade-local --kit . --bot <repository> --driver process

It plays a practice trial against the house engines and prints the Elo.
