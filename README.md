# Supplier Performance Scorecard

An Excel-based supplier scorecard that evaluates 40 suppliers on quality, delivery, and responsiveness, combines those into a weighted composite score, assigns letter grades, and flags underperformers for review.

## What it does

- Normalizes three performance metrics onto a common 0-100 scale where higher always means better
- Combines them into a single weighted composite score
- Assigns A-F letter grades with conditional formatting to surface problem suppliers
- Provides a lookup tool that returns any supplier's full profile from an ID
- Cross-tabs performance against supply chain risk tier

## Scoring methodology

Three raw metrics feed the model:

| Metric | Raw range | Direction |
|---|---|---|
| On-time delivery % | 70-99 | Higher is better |
| Defect rate % | 0-8 | Lower is better |
| Avg response days | 1-14 | Lower is better |

Defect rate and response time are inverted during normalization so that all three scores point the same way before they are combined.

**Weights:**

| Component | Weight | Reasoning |
|---|---|---|
| Quality | 50% | Highest consequence of failure. A defect can become a field failure or recall. |
| Delivery | 30% | Real cost, but a delay is recoverable in a way a defect is not. |
| Responsiveness | 20% | Softest and most subjective of the three. |

Weights are assigned by consequence of failure rather than equally. This is a judgment call, and a different organization could justify a different split.

**Grade thresholds:** A ≥ 85, B ≥ 70, C ≥ 55, D ≥ 40, F below 40.

## Results

Grade distribution across 40 suppliers:

| Grade | Count |
|---|---|
| A | 2 |
| B | 8 |
| C | 9 |
| D | 17 |
| F | 4 |

**Finding:** Cross-tabbing grades against FOCI risk tier showed failing suppliers concentrated in the high-risk group. Three of the four F-grade suppliers are HIGH RISK, one is MEDIUM, and none are LOW. Neither A-grade supplier is high risk. Risk exposure and performance problems sit on overlapping vendors, which turns a supplier-by-supplier conversation into a portfolio question.

**Where the data did not support a conclusion:** Average composite score by country ranged from 73.4 (China) down to 47.6 (USA), but both figures rest on 4 and 5 suppliers respectively. Those samples are too small to claim a country-level pattern, and the count column is included in the pivot specifically so that limitation is visible rather than hidden.

## Excel techniques used

- Pivot tables with Average and Count aggregations
- XLOOKUP with fallback handling for invalid inputs
- IFS for tiered grade logic
- Conditional formatting to flag underperformers
- Static value conversion to prevent volatile functions from redrawing results

## Workbook structure

| Sheet | Contents |
|---|---|
| suppliers_scored | Raw supplier data, normalized scores, composite, grade |
| Pivots | Performance by country, grade distribution by risk tier |
| Lookup | Enter a supplier ID to return that supplier's full profile |

## Data

The 40-supplier dataset is synthetic and carries over from a prior supplier risk scoring project. Performance metrics were generated within realistic ranges. Because the data is fabricated, the findings above demonstrate the analytical method rather than describing a real supplier base.
