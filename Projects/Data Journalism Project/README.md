# Pedal&Co Relaunch Analytics (2015–2018)

This repository contains a **data-driven relaunch strategy** for **Pedal&Co**, a bicycle company founded in 2015 that ceased operations in 2018 and is now planning a relaunch.  
Using **Tableau**, we analyzed historical sales, manpower, and customer data to provide **actionable insights** and **16 strategic recommendations** for inventory planning, staffing, and marketing.

---

##  Project Overview

**Objective**  
Leverage historical sales and operational data to:
- Identify the **best-selling products** and **slow-moving inventory**
- Recommend **top-performing staff** to rehire for the relaunch
- Understand **customer loyalty patterns** and target profitable segments
- Prioritize **stores and regions** for reopening based on past performance

**Scope**
- **Products** → Revenue drivers, slow/no-sale SKUs, promotional candidates
- **Manpower** → Staff productivity, rehiring strategy, store prioritization
- **Customers** → Loyalty segmentation, geographic distribution, retention focus

---

##  Dashboards

### **1. Product Sale Dashboard**
<img width="2216" height="1316" alt="Screenshot 2025-09-06 135518" src="https://github.com/user-attachments/assets/f5400469-a9bb-4893-abf9-dbf535aae686" />


**Key Features**
- **Pareto Analysis** → Visualizes the top 20% products contributing ~80% of sales  
- **No-Sale Products** → Highlights products with stock but **zero historical sales**
- **Lowest-Sale Products** → Identifies SKUs suitable for bundling or promotions
- **Category-Level Sales** → Shows the most profitable categories

**Business Use**  
Helps identify **high-priority SKUs** for initial stocking, promotions for underperformers, and products to phase out.

---

### **2. Manpower Dashboard**
<img width="2215" height="1308" alt="Screenshot 2025-09-06 135606" src="https://github.com/user-attachments/assets/0bf95fe1-376c-4cda-a2b9-2ac8730034c6" />


**Key Features**
- **Staff Order Handlability** → Ranks staff based on order-handling efficiency
- **Staff Performance Trends** → Shows quarterly performance over 2016–2018
- **Store Performance Pie Chart** → Highlights high-performing store locations
- **Monthly Store Sales** → Reveals seasonal trends for smarter inventory planning

**Business Use**  
Supports **rehiring decisions**, **store reopening priorities**, and **staff allocation** to maximize operational efficiency.

---

### **3. Customer Dashboard**
<img width="2229" height="1310" alt="Screenshot 2025-09-06 135646" src="https://github.com/user-attachments/assets/c470ec09-ee8d-46df-89b6-8437c78bf0ad" />


**Key Features**
- **Top-N Customers** → Identifies the most valuable revenue-driving customers
- **Customer Loyalty Breakdown** → Shows **repeat vs. one-time buyers**
- **Customer Map** → Visualizes geographic distribution of customers
- **Dynamic Filtering** → Interactively drill down by store, state, year, and zip code

**Business Use**  
Helps **retain top customers**, improve **repeat purchase rates**, and target **high-density geographic clusters** for marketing.

---

## Data Model

The data follows a **star schema** centered on the `order_items` table.

**Core relationships:**
- `order_items` → `orders` → `customers`
- `order_items` → `products` → `categories`, `brands`, `stocks`
- `orders` → `stores`
- `stocks` → `store-stocks`

**Source**: The full analysis report is available at [here](docs/Report.md)

## Conclusion 
This project delivers a comprehensive, data-driven relaunch strategy for Pedal&Co by leveraging historical sales, manpower, and customer data. Through detailed Tableau dashboards and analysis, we identified top-performing products, high-value customers, and priority stores while uncovering opportunities for promotions and customer retention.

With 16 actionable insights and recommendations, the project provides clear guidance for optimizing inventory planning, staff rehiring, and targeted marketing to ensure a successful relaunch and sustainable long-term growth.


