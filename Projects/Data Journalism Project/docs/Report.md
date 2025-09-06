
# Pedal&Co Relaunch — Analysis Report

## 1) Objective
Use historical data (2015–2018) to inform the relaunch plan and candidate rehiring.

## 2) Scope
- **Products**: identify revenue drivers, slow/no-sale items, promo candidates
- **Manpower/Stores**: staff productivity, store prioritization, monthly seasonality
- **Customers**: top customers, loyalty split, geography for targeted marketing

## 3) Method (Tableau)
- Relationship model around `order_items`; extracts refreshed from Excel
- Calculated fields for Sales, loyalty, best-seller flag, clean sorting measures
- Dashboard actions: cross-filters; state filters handled via context to avoid granularity issues

## 4) Key Findings (summarized)
- A small set of products & categories generated the majority of sales (Pareto)
- Several SKUs held stock but recorded **no sales** → promo/clearance opportunity
- Clear set of **low-sale** products → bundle/upsell candidates
- Distinct top-performing staff and stores; monthly patterns present
- High share of **one-time buyers**; repeat base is valuable but smaller than ideal
- Customers cluster in **TX, CA, NY**; overlaps with stronger stores

## 5) 16 Insights & Recommendations (detailed)
**Product**
1. **Prioritize key SKUs** from Pareto for initial stock & ads (fastest revenue impact).
2. **Promote no-sale SKUs** with in-stock quantity via clearance/BOGO to recover cash and shelf space.
3. **Cull or redesign persistent underperformers** to cut carrying cost and simplify catalog.
4. **Lean into top categories** for merchandising and paid campaigns; mirror historic demand.

**Manpower & Stores**
5. **Rehire top handlers** (treemap leaders) for launch teams; they shorten ramp-up.
6. **Staff high-priority stores first**; pair best staff with best stores to compound effect.
7. **Targeted coaching** based on quarterly performance trends; keep strong trajectories.
8. **Reopen high-yield stores** first (store mix/pie + monthly sales) to accelerate payback.

**Customers**
9. **VIP program for Top-N** customers (early access, tiered benefits) to seed day-1 sales.
10. **Fix the one-time bias**: post-purchase journeys, email/SMS win-backs, next-order coupons.
11. **Formal loyalty program** (points/tiers) to increase repeat rate and CLV.
12. **Geo-target TX/CA/NY** with localized promos and store events; matches density & history.

**Sales & Promotions**
13. **Align promos to monthly seasonality** seen in store sales; front-load inventory accordingly.
14. **Feature best-sellers in all channels** (site, POS, ads) to maximize conversion.
15. **Bundle low-sellers with winners** (accessory packs, cross-sell) to move stock while preserving margin.
16. **Track loyalty KPIs monthly** (% repeat, CAC-to-CLV) and iterate on program mechanics.

## 6) Risks & mitigations
- **Data drift** after relaunch → schedule monthly extract refresh + QA checklist.
- **Overfitting to legacy mix** → A/B test new SKUs while keeping core best-sellers.
- **Action bias from map filters** → use context filters & worksheet targeting to avoid blank views.

## 7) Next steps
- Pilot reopening at top 1–2 stores with top staff
- Launch loyalty + VIP offers to Top-N customers
- 90-day review: repeat rate uplift, stockout %, promo ROI

## 8) Appendix
<img width="2216" height="1316" alt="image" src="https://github.com/user-attachments/assets/1b56789f-178b-44b9-829b-e54d2e1a2a2b" />

**Product Sale Dashboard**

<img width="2215" height="1308" alt="image" src="https://github.com/user-attachments/assets/7a4a142c-12f1-4c59-aead-3e2d55f8a0dc" />

**Manpower Dashboard**

<img width="2229" height="1310" alt="image" src="https://github.com/user-attachments/assets/50c44b56-f755-4920-ba80-45cfea3f177f" />

**Customer Dashboard**

**Source**: See the full data story [here](https://public.tableau.com/app/profile/zwe.thiha.naung/viz/AY2025S1IT2383Assignment_243979B/Story1)

- Formulas: see `CalculatedFields.md` **Source**: [here](CalculatedFields.md)
