# Reproduction Steps

1) Open `tableau/PedalCo_Relaunch.twb` in Tableau Desktop.
2) Point to `data/Pedal&CoDataset.xlsx`.
3) Confirm relationships as in `docs/DataModel.md`.
4) Create/verify calculated fields from `docs/CalculatedFields.md`.
5) Build dashboards:
   - Product: Pareto (running sum %), No-Sale (filter = 'No Sales'), Lowest-Sale (sort by Clean Sales asc)
   - Manpower: treemap (orders handled by staff), small-multiples lines by staff/quarter, store sales by month
   - Customer: Top-N (parameter), Loyalty pie (Customer Type with CNTD(Customer ID)), Map by state
6) Story:
   - Intro → Product → Manpower → Customer → Conclusion
7) Dashboard actions:
   - Enable “Use as Filter” where needed
   - For Map → apply to specific worksheets OR add State as **context filter** instead of Detail
8) Export screenshots to `assets/` and publish.
