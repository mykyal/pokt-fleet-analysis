# Fleet Observatory

Explore historical Pocket Network Supplier fleets, compare recorded payments with an equal-share reference, and understand session selection.

**[Open the application](https://pokt-fleet-analysis.vercel.app/)**

An independent research prototype—not an official network product.

## What it does

- Find fleets using owner addresses, Supplier addresses, domains or hostnames.
- Compare recorded gross payments with an equal-share reference.
- Explore differences across services, Suppliers, Applications and time.
- Inspect individual sessions and historical endpoint associations.
- Explore fleet-size selection scenarios and export the underlying evidence.

## Data

The application contains a saved mainnet snapshot covering **6 September–5 October 2026 UTC** across eight services: `arb-one`, `base`, `bsc`, `eth`, `opbnb`, `poly`, `robinhood` and `solana`.

Two complementary datasets answer different questions:

| Dataset | Purpose | Coverage |
|---|---|---|
| Recorded settlements | Compare payments with equal share in sessions where the fleet was selected | 29,448 sessions and 851,096 settled Supplier claims |
| Sampled selection | Examine selection against historical eligible populations | 4,080 distinct sessions from four daily checkpoints |

The datasets can overlap; their session counts should not be added.

**The website does not automatically refresh.** Opening it reads the saved data, not a live API feed. A separately labelled fictional preview is available at `?dataset=preview`.

## Understanding the comparison

**F = total recorded gross payments ÷ total equal-share reference**

For example, if a fleet received 30 POKT against an equal-share reference of 20 POKT, F is **1.5**, or **50% above equal share**.

Equal share divides each session’s Supplier payout pool evenly across its selected Suppliers. Comparisons use sums across sessions—not averages of individual F scores.

F is not a measure of net profit, investment return or service quality. Historical tests and uncertainty ranges are not forecasts.

## Collection and reproducibility

Since 27 October 2026, the collectors use Pocketdex’s session catalogue at `data.pocket.network/graphql` for rosters, payouts, historical Supplier configurations, eligibility and parameters.

The updated collection reproduced the reviewed month’s settlement records without changing its financial contents.

- [Python collection code](collector/)
- [Settlement collection notebook](notebooks/pokt_settlement_collection.ipynb)
- [Monthly claims diagnostic notebook](notebooks/pokt_monthly_claims_check.ipynb)
- [Collection methodology and sources](docs/data-collection.md)

The saved dataset is included. You do not need to collect it again to run the application.

## Important limitations

- Recorded settlements do not prove that every network payment is represented.
- Uncovered sampled payout outcomes remain unknown, rather than being assumed zero.
- Selection scenarios depend on historical eligibility and modelling assumptions.
- Domains identify recorded endpoint associations—not verified business ownership, geography or physical server counts.
- Sparse results may remain unavailable or unranked.

## Run locally

Use Node.js 22 and Python. Run these commands from the repository folder:

```sh
npm run build
python -m http.server 8000 --directory dist
```

Open **http://localhost:8000**. Serve the complete `dist` folder rather than opening its HTML file directly.

To run the main checks:

```sh
npm test
python -m unittest discover -s tests -p 'test_*.py'
npm run check
```

## Further documentation

- [How the two datasets work](docs/settlement-integration.md)
- [Terminology](docs/terminology.md)
- [Endpoint parsing](docs/endpoint-model.md)
- [Validation and site audit](docs/site-audit.md)
- [Browser review checklist](docs/review-guide.md)
