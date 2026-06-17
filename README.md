# Data Task

## Introduction

This is a task to build a small but production-minded data pipeline incorporating:

- ingestion of raw, imperfect source data
- cleaning, validation and standardisation
- transformation and modelling into an analytics-friendly structure
- making the modelled data queryable to answer business questions
- testing

You may use **whatever language and tools you are most productive in** — for example
Python (pandas / Polars / PySpark), SQL with DuckDB, dbt, or any combination. You can
store the modelled data however you think is suitable (e.g. Parquet, DuckDB, SQLite, a
local Postgres). There is no requirement to use any particular framework or cloud
service. We are far more interested in how you reason about data than in which tool you
reach for.

The raw data in `data/` is deliberately messy and reflects the kind of real-world
inconsistencies you would meet on the job.

## The Data

Two source files are provided in `data/`:

### `orders.csv`

One row per vehicle order across several European markets.

- `order_id` — integer
- `vehicle_id` — integer (references `vehicles.csv`)
- `market` — string
- `currency` — string
- `channel` — string
- `order_date` — date
- `delivery_date` — date (may be absent)
- `order_status` — string
- `sale_amount` — the sale value
- `customer_email` — string

### `vehicles.csv`

Reference data, one row per vehicle.

- `vehicle_id` — integer
- `make` — string
- `model` — string
- `segment` — string
- `fuel_type` — string
- `list_price_gbp` — integer

> The data contains a representative set of quality issues. Part of the task is to
> discover them; we have deliberately not listed them all here.

## Minimum Requirements

- Ingest both source files.
- Clean, validate and standardise the data so it is fit for analysis — handling the
  quality issues you find and documenting the decisions you make.
- Model the result into a clean, analytics-friendly structure of your choosing, and
  explain why you chose it.
- Using your modelled data, answer the following business questions:
  1. Total completed sales value **by market and by month** (in a single, consistent
     currency).
  2. The top 5 **models** by units sold.
  3. The average number of days **from order to delivery**, by market.
  4. The share of orders placed through each **channel**.
- Provide a suite of tests covering your cleaning/validation logic and your
  transformations.
- A `README.md` explaining your approach, the assumptions and trade-offs you made, and
  how to run the pipeline and the tests.

## Optional / Discussion

You do **not** need to build these — a short written answer in your README is enough.
We will discuss them with you.

- How would you make this pipeline **incremental and idempotent** so it can run daily
  against a growing source, without reprocessing everything or creating duplicates?
- How would you **partition** the modelled data, and why?
- How would you expose this data for **self-serve BI** so that different teams get
  **consistent metrics** (e.g. everyone calculating "completed sales" the same way)?
- How would you **monitor data quality and freshness** in production, and what would
  you alert on?
- A source system starts sending a **changed (breaking) schema**. How would you detect
  it and how should the pipeline behave?
- What **data governance / privacy** considerations apply here (the data spans UK and EU
  markets and includes a customer identifier)?

## Submission

Here's what you'll need to send us:

- A link to a **public** GitHub repo that you have created, containing the code.
- It should contain a suite of tests (using whichever test framework you prefer).
- It should contain a `README.md` explaining your approach, how to run the pipeline,
  and how to run the tests.
- Your written answers to the discussion points above (in the README is fine).

**The core build should take around 2-3 hours.** Please don't gold-plate it — we would
rather see clear thinking, sensible trade-offs and good tests than a large unfinished
system. If you run short on time, tell us in your README what you would do next.
