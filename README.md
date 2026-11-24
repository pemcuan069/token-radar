# Token Radar

[![make.fun bounty](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01)
[![make.fun rank](https://make.fun/badge/token-radar-01/pemcuan069/token-radar/rank.svg)](https://make.fun/bounty/token-radar-01)
[![make.fun reward](https://make.fun/badge/token-radar-01/pemcuan069/token-radar/reward.svg)](https://make.fun/bounty/token-radar-01)

A pre-token launch radar for make.fun's [Build the best token launch radar](https://make.fun/bounty/token-radar-01) bounty. It ranks the 40 watchlist protocols and every rankable pre-token protocol below the watchlist floor by implied value, and gives each one a farm plan.

## How it works

Implied value is priced off each protocol's own live-token peers, not one flat multiple. For every category, the model takes the median mcap/TVL of the live-token protocols in that category, shrinks it toward the market-wide median, and caps it, so a thin category cannot price itself off one outlier. Growth over seven days and time running with no token adjust the price from there. The dashboard names the peers behind every row, and the page recomputes each row from the same figures board.json carries.

## Run it

Node 22, standard library only, no install:

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input ../input/snapshot.json
```

That writes `board.json`, `data.js`, `dashboard/`, `screenshots/` and `dossier.json` to the output directory.

## Layout

- `main.ts` — reads the sealed snapshot, scores the board, writes the output.
- `lib/model.ts` — the peer-priced model, the farm plans, and the board checks.
- `vendor/makefun-board.ts` — make.fun's dossier library, copied from the kit.
- `dashboard/` — the static page: board, detail view, filters, and the model with its peer table.
- `screenshots/` — the board, a detail view, and a filtered view.
