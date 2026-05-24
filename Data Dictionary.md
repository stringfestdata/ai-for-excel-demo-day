# Wholesale Customers — Data Dictionary

The dataset used in the AI for Excel Demo Day live demo.

## What it is

440 anonymized customers of a wholesale distributor based in Portugal, recording one row per customer and annual spend across six product categories. It's the **UCI Wholesale Customers Dataset**, originally published by Margarida G.M.S. Cardoso (ISCTE Business School, Lisbon) and donated to the UCI Machine Learning Repository in 2014. Widely used as a teaching dataset for segmentation, clustering, and — as we use it here — for showing why "tabular" doesn't automatically mean "machine-readable."

| Property | Value |
|---|---|
| Rows | 440 |
| Columns | 8 |
| File | `wholesale-customers.xlsx` |
| Source | UCI ML Repository (Cardoso, 2014) |
| Original currency | Monetary units (m.u.) — the original Cardoso paper used Portuguese euros |

## Columns

| # | Column | Type | Meaning |
|---|---|---|---|
| 1 | `Channel` | integer code | **Customer type.** `1` = HoReCa, `2` = Retail. See translation table below. |
| 2 | `Region` | integer code | **Customer location.** `1` = Lisbon, `2` = Oporto (Porto), `3` = Other region. |
| 3 | `Fresh` | integer | Annual spend on fresh products (m.u.) |
| 4 | `Milk` | integer | Annual spend on milk products (m.u.) |
| 5 | `Grocery` | integer | Annual spend on grocery products (m.u.) |
| 6 | `Frozen` | integer | Annual spend on frozen products (m.u.) |
| 7 | `Detergents_Paper` | integer | Annual spend on detergents and paper products (m.u.) |
| 8 | `Delicassen` | integer | Annual spend on delicatessen products (m.u.). **Note:** misspelled in the original dataset — should be "Delicatessen." We keep the original spelling so the file matches every other copy of this dataset on the internet. |

## What the codes mean

### Channel

| Code | Label | What it means |
|---|---|---|
| `1` | **HoReCa** | **Ho**tel / **Re**staurant / **Ca**fé. European wholesale jargon for the food-service buyer segment — restaurants, hotels, catering. |
| `2` | **Retail** | Retail grocers — supermarkets, corner stores, neighborhood shops. |

### Region

| Code | Label |
|---|---|
| `1` | Lisbon |
| `2` | Oporto (Porto) |
| `3` | Other region |

## Quick stats (annual spend per customer)

| Column | Min | Median | Mean | Max | Total |
|---|---:|---:|---:|---:|---:|
| Fresh | 3 | 8,504 | 12,000 | 112,151 | 5,280,131 |
| Milk | 55 | 3,627 | 5,796 | 73,498 | 2,550,357 |
| Grocery | 3 | 4,755 | 7,951 | 92,780 | 3,498,562 |
| Frozen | 25 | 1,526 | 3,071 | 60,869 | 1,351,650 |
| Detergents_Paper | 3 | 816 | 2,881 | 40,827 | 1,267,857 |
| Delicassen | 3 | 965 | 1,524 | 47,943 | 670,943 |

### Counts and totals by channel / region

| | Customers | Total spend (m.u.) |
|---|---:|---:|
| Channel 1 — HoReCa | 298 | 7,999,569 |
| Channel 2 — Retail | 142 | 6,619,931 |
| **All channels** | **440** | **14,619,500** |

| Region | Customers |
|---|---:|
| 1 — Lisbon | 77 |
| 2 — Oporto | 47 |
| 3 — Other | 316 |

## Why we use it for the demo

Three things make this dataset perfect for showing where AI in Excel stumbles:

1. **Channel and Region are integer codes**, not labels. A language model looking at "Sum of Channel" will happily add 1s and 2s together — meaningless, but it looks like a number.
2. **There is no "sales" column.** Spend is split across six product categories. "Total sales by channel" requires building a derived column first.
3. **The data is wide, not tidy.** Six spend columns per row means the tool has to figure out which columns to add, in which order, with which grouping. That's a deterministic-tool job (Power Query), not a probabilistic-tool job.

These three quirks are why "Find total sales by channel" in Analyze Data returns something confidently wrong — and why the Power Query fix (replace the codes, unpivot the six spend columns, group by channel) is the lesson the hour is built around.

## Citation

Cardoso, M. (2014). *Wholesale customers* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5030X
