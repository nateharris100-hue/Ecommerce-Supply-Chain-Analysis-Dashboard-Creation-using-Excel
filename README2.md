# Supply Chain Operations Efficiency Dashboard (Tableau)

An interactive Tableau dashboard analyzing delivery performance across shipping modes on a public ecommerce supply chain dataset.

**[→ View the live dashboard on Tableau Public](https://public.tableau.com/app/profile/nathaniel.harris8003/viz/SupplyChainOperationsEfficiencyDashboard/SupplyChainOperationsEfficiencyDashboard)**

---

## About this repository

This is a fork of [shreya1m/Ecommerce-Supply-Chain-Analysis-Dashboard-Creation-using-Excel](https://github.com/shreya1m/Ecommerce-Supply-Chain-Analysis-Dashboard-Creation-using-Excel). **The Excel workbooks, documentation and dataset in this repo are the upstream authors' work** — I forked it to work with the dataset.

My contribution is the Tableau dashboard linked above, and this file.

**Dataset:** DataCo Smart Supply Chain dataset (public) — 70,000 orders × 53 fields, Jan 2015 to Sep 2017, spanning 163 countries, 118 products, 50 categories and 15,190 customers. Total sales $14.26M.

---

## The finding

On-time performance gets *worse* as the promised speed gets faster — and the cause is the promise, not the shipping.

| Shipping mode | Orders | On-time | Late-delivery risk | Actual days | Scheduled days |
|---|---|---|---|---|---|
| Standard Class | 41,802 | **60.2%** | 38.0% | 4.0 | 4.0 |
| Same Day | 3,828 | 51.9% | 46.1% | 0.5 | 0.0 |
| Second Class | 13,705 | 20.2% | 76.7% | 4.0 | 2.0 |
| First Class | 10,665 | **0.0%** | 95.4% | 2.0 | 1.0 |

Read the last two columns together. **Standard Class is the only mode whose scheduled and actual shipping days match** — it promises 4 days and takes 4, and it is the only mode with a majority on-time rate.

Every premium tier is scheduled against a target it never meets. First Class is booked at 1 day and averages 2, which is why it posts a 0% on-time rate: it is not slow, it is mis-promised. Second Class is booked at 2 days and averages 4.

Across the whole book, 54.8% of orders carry late-delivery risk and actual shipping averages 3.50 days against 2.93 scheduled — a systematic 0.57-day planning gap.

Delivery status mix: 54.8% late, 23.0% advance, 17.9% on time, 4.3% canceled.

**Recommendation:** re-baseline delivery promises on observed transit times per mode rather than on carrier tier. Most of the "late" volume is a scheduling artifact, and customers paying for First Class are being quoted a date the lane has never once hit.

---

## Dashboard features

- 4 KPI cards — on-time rate, late-delivery risk, cost per day, delivery variance
- Shipping-mode performance comparison
- Delivery time trend across the three-year period
- Cost vs. speed scatter analysis
- Late-delivery risk breakdown by mode
- Planning accuracy (scheduled vs. actual) by mode
- Interactive filter for drilling into a single shipping mode

## Method note

**On-time** is defined as `Days for shipping (real) <= Days for shipment (scheduled)` — did the order arrive within the window it was promised. **Late-delivery risk** is the dataset's own `Late_delivery_risk` flag. The two differ slightly because the flag is assigned at order time while on-time is measured on the outcome.

Figures above are recomputed directly from `DataCoSupplyChainDataset.csv` in this repo and are reproducible from it.

---

**Nathaniel Harris** — Operations Management & Business Analytics / Supply Chain Management, University of Maryland
