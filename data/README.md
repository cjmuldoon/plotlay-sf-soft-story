# The data

Made from DataSF (PDDL) and California Geological Survey (CC BY) data, see [`../NOTICE`](../NOTICE); our tables and shapes are CC BY 4.0.

- `tables/parcels.csv`: one row per parcel on the program's list (4,901). `blklot` (block and lot), `tier` (I to IV as 1 to 4), `status` (Complete, Non-compliant, Newly added, from the list as of 2026-10-07), `address`, `rows` (list rows for the parcel), `completed` (the earliest completed date of a completed soft story permit), `first_filed`, `year_done` (blank when not complete or no permit date), `liquefaction` (yes, no, unknown), `liq_share` (share of the parcel's area in a zone).
- `tables/parcels_by_year.csv`: one row per parcel and year 2014 to 2026: `done` (1 once retrofitted), `state` (what the map shows that year).
- `tables/share_done_by_year.csv`: by year and group (All, in a liquefaction zone, outside): parcels, done by then, the share, done that year.
- `geometry/soft_story_parcels.*`: the parcels, keyed by `blklot`. `geometry/liquefaction_zones.*`: the zones in San Francisco, merged and split into 43 pieces, keyed L01 up.
