# Complaint Router

Financial companies receive consumer complaints as free text and have to send each one to the product team that can resolve it. Manual triage is slow, and a misrouted complaint loses days. Complaint Router reads a complaint at intake and returns one of nine product queues with a confidence score; confident cases are routed automatically and the rest go to manual triage. It is trained on the CFPB Consumer Complaint Database narratives archive (December 2011 to August 2026), replayed month by month to simulate new data. Each new month is versioned, checked, used to retrain a candidate model and compared with the production model before a person promotes it, and drift is monitored so that quality problems are noticed early.

The design document is [docs/design.md](docs/design.md).

## Quick start

Requirements: Python 3.12+, [uv](https://docs.astral.sh/uv/), make.

```bash
make setup
make lint
```

`make setup` creates `.venv` from `uv.lock`; `make lint` runs `ruff check .`. To run the same check before each commit: `uv run pre-commit install`.

## Maturity scorecard

| Property | Evidence a reviewer checks | Added in |
|---|---|---|
| Repository reproducible from a clean clone | CI is green; `make setup` and `make lint` succeed on a fresh clone | Lab 1 |
| Design document exists and is current | [docs/design.md](docs/design.md) follows the template, every section filled or marked as an assumption | Lab 1 |

## Repository layout

```
.github/workflows/lint.yml   CI: make setup and make lint on every push
.pre-commit-config.yaml      ruff check before commit
docs/design.md               design document with diagrams
src/complaint_router/        package, code starts in Lab 2
Makefile                     setup, lint
pyproject.toml               project and dev tools
uv.lock                      locked environment
```

## Data

CFPB Consumer Complaint Database narratives archive, US government public data:
https://www.consumerfinance.gov/foia-requests/foia-electronic-reading-room/cfpb-consumer-complaint-database-narratives-archive/

The data is not stored in git. Lab 2 adds the DVC pull command.
