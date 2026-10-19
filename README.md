# Complaint Router

Financial companies receive consumer complaints as free text and must send each one to the product team that can resolve it; manual triage is slow and misrouted complaints lose days. Complaint Router reads a complaint at intake and returns one of nine product queues with a confidence score, routing confident cases automatically and sending uncertain ones to human triage. It is trained on the CFPB Consumer Complaint Database narratives archive (December 2011 – August 2026), replayed month by month to emulate new data. Each new month is versioned, quality-checked, used to retrain a candidate model, and compared with the production model before a human promotes it. Drift in what people complain about and how they write is monitored so that a person notices before routing quality degrades.

The full design is in [`docs/design.md`](docs/design.md).

## Quick start

Requirements: Python 3.12+, [`uv`](https://docs.astral.sh/uv/), `make`.

```bash
make setup   # creates .venv from uv.lock
make lint    # ruff check .
```

Optional, once per clone: `uv run pre-commit install` to run the same linter before every commit.

## Maturity scorecard

| Property | Evidence a reviewer checks | Added in |
|---|---|---|
| Repository reproducible from a clean clone | CI is green; `make setup` and `make lint` succeed on a fresh clone | Lab 1 |
| Design document exists and is current | [`docs/design.md`](docs/design.md) follows the template, every section filled or marked as an assumption | Lab 1 |

## Repository layout

```
.
├── .github/workflows/lint.yml   # CI: make setup + make lint on every push
├── .pre-commit-config.yaml      # same ruff check, before commit
├── docs/design.md               # design document with diagrams (Mermaid)
├── src/complaint_router/        # package (code arrives in Lab 2)
├── Makefile                     # setup, lint
├── pyproject.toml               # project + pinned dev tools
└── uv.lock                      # locked environment
```

## Data

CFPB Consumer Complaint Database Narratives Archive, US government public data:
https://www.consumerfinance.gov/foia-requests/foia-electronic-reading-room/cfpb-consumer-complaint-database-narratives-archive/
Data is not stored in git; Lab 2 adds the DVC pull command.
