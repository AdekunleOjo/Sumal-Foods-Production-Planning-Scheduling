# FMCG Production Planning & Scheduling System with Python

A manufacturing analytics python portfolio project exploring how demand forecasting, material requirements planning, and production capacity analysis can support seasonal production planning in the biscuit industry.

**Planning horizon:** 19 October to 31 December 2026  
**Industry:** FMCG / Biscuit Manufacturing  
**Tools:** Python, Pandas, NumPy, Matplotlib, PuLP, Jupyter Notebook  
**Project status:** Demand forecasting and material planning completed; production optimization in progress.

> **Data disclaimer:** This is an independent portfolio project using simulated data and illustrative operating assumptions. It does not use actual Sumal Foods Limited production records or represent its internal operations.

## 1. Business Context

Seasonal demand creates additional planning pressure for FMCG manufacturers. Production teams must translate demand forecasts into material requirements, determine whether available resources can support the required output, and develop feasible production plans.

In biscuit manufacturing, this involves coordinating several products with different production rates, raw material requirements, and packaging needs while accounting for production line capacity.

This project develops a Python-based planning workflow around a simulated biscuit manufacturing operation in Ibadan, Nigeria, using Sumal Foods Limited as the industry context.

The central business question is:

**How can a manufacturer translate seasonal product demand into a material and production plan that makes the best use of available capacity?**

## 2. Project Workflow

The notebook follows a modular planning approach, moving from demand estimation to material planning and then toward production optimization.

```text
Product Master Data
        |
        v
Weekly Demand Simulation
        |
        v
Demand Analysis and Visualization
        |
        v
Bill of Materials (BOM)
        |
        v
Material Requirements Planning
        |
        v
Opening Inventory and Shortage Analysis
        |
        v
Production Demand and Line Capacity
        |
        v
Production Optimization and Scheduling
        |
        v
Planned Output, Resource Utilization
and Production Schedule
```

The first stages establish the planning inputs required for the later optimization model.

## 3. Module 1: Demand Forecasting and Analysis

The first module generates a weekly demand forecast for four simulated biscuit products over the Q4 2026 planning horizon.

Products included:

- Yale Cabin 25g
- Yale Glucose 35g
- Yale Speedy Chocolate 40g
- Sumal Shortcake

The demand simulation combines baseline weekly demand assumptions, a progressive seasonal growth factor, and random variation to create a more realistic planning dataset than a fixed demand schedule.

### Methodology

1. Define the product master data and baseline weekly demand.
2. Generate weekly planning periods from 19 October to 31 December 2026.
3. Apply seasonal growth and random demand variation.
4. Summarize demand by product and week.
5. Visualize demand trends to support capacity and material planning.

### Demand Trend

![Weekly demand trend](images/weekly_demand_trend.png)

*Figure 1. Simulated weekly demand across the four biscuit products.*

### Business Relevance

The demand profile provides the starting point for translating expected sales requirements into production quantities. It also helps identify products and planning periods that may require closer attention when allocating production capacity and estimating material needs.

The forecast is simulated for demonstration purposes and should not be interpreted as a sales forecast for the actual company.

## 4. Module 2: Material Requirements Planning (MRP)

The second module connects product demand to a simulated bill of materials (BOM). This makes it possible to estimate how much of each input would be required to satisfy the total forecast demand.

### Materials Included

- Wheat flour
- Sugar
- Cocoa powder
- Vegetable fat
- Packaging film

Each product has its own illustrative material consumption rates. The notebook multiplies total forecast demand by the relevant BOM quantities, aggregates requirements by material, and compares the resulting requirements with assumed opening inventory.

### Planning Logic

For each material:

**Gross material requirement**

`Total product demand × Material quantity per pack`

**Estimated material shortage**

`Maximum of (Gross requirement − Opening inventory, 0)`

The model then flags materials whose aggregate requirements exceed the available opening stock.

### Material Shortage Analysis

![Material shortage analysis](images/material_shortage_analysis.png)

*Figure 2. Comparison of estimated gross material requirements and opening inventory.*

### Business Relevance

The shortage analysis helps identify materials that may need replenishment or further investigation before a production plan is finalized. It also demonstrates how demand forecasting and inventory information can be connected within one planning workflow.

**Current limitation:** This version uses aggregate requirements across the full planning horizon. It does not yet model weekly inventory balances, supplier lead times, scheduled receipts, safety stock, or the exact timing of material stockouts.

## 5. Module 3: Production Demand and Capacity Planning

The third module establishes the initial inputs for evaluating whether simulated production resources can support daily demand.

The assumed daily demand is:

| Product | Daily demand (packs) |
|---|---:|
| Yale Cabin 25g | 180,000 |
| Yale Glucose 35g | 150,000 |
| Yale Speedy Chocolate 40g | 120,000 |
| Sumal Shortcake | 100,000 |
| **Total** | **550,000** |

Two simulated production lines are defined, each with different production rates depending on the product being manufactured.

The model includes six line and product combinations, with assumed production rates ranging from 6,000 to 10,000 packs per hour.

### Planning Considerations

The next stage will evaluate:

- Whether daily demand can be met within available production hours.
- How products should be allocated across compatible production lines.
- How production quantities affect line utilization.
- How to identify capacity constraints and potential unmet demand.
- How to incorporate changeover and cleaning time into the schedule.

These rates and demand values are illustrative assumptions, not verified factory operating data.

## 6. Planned Optimization and Scheduling

The next development stage is to formulate a production optimization model using PuLP, a Python library for mathematical optimization.

The intended model will build on the demand and capacity inputs already prepared in the notebook.

Planned capabilities include:

- Allocating production quantities across eligible lines.
- Meeting product demand subject to available production capacity.
- Evaluating production time requirements.
- Incorporating sequence-dependent product changeovers and cleaning assumptions.
- Generating a production schedule and visualizing the proposed sequence.
- Reporting capacity utilization and any unmet demand.

The scheduling assumptions will distinguish minor product transitions from major transitions requiring more extensive cleaning. These rules will be documented explicitly so that the model's results can be interpreted and reproduced.

These optimization and scheduling capabilities are planned work, not completed functionality in the current version.

## 7. Technology Stack

| Technology | Application |
|---|---|
| Python | Planning logic and calculations |
| Pandas | Data preparation, grouping, merging, and reporting |
| NumPy | Demand simulation and numerical calculations |
| Matplotlib | Demand and material planning visualizations |
| Jupyter Notebook | Step-by-step analysis and documentation |
| PuLP | Planned mathematical optimization model |

## 8. Current Project Status

| Component | Status |
|---|---|
| Product master data and planning horizon | Completed |
| Weekly demand simulation | Completed |
| Demand summaries and visualization | Completed |
| Bill of materials and opening inventory | Completed |
| Aggregate material requirements calculation | Completed |
| Material shortage analysis | Completed |
| Daily demand and production rate inputs | Prepared |
| Production optimization model | In progress |
| Changeover-aware scheduling | Planned |
| Production schedule and Gantt chart | Planned |
| Final capacity and utilization reporting | Planned |

## 9. Key Takeaways

This project demonstrates an end-to-end approach to structuring manufacturing planning data, starting with demand and connecting it to material requirements and production capacity.

The current implementation establishes the data preparation and planning foundation. Completing the optimization and scheduling modules will extend it into a more integrated decision-support workflow.

The project is designed to demonstrate practical applications of Python and operations analytics in FMCG manufacturing, particularly in demand planning, materials planning, production capacity, and scheduling.

## 10. Repository Structure

```text
FMCG-Production-Planning-Scheduling/
│
├── Sumal_Q4_2026_Production_Planning.ipynb
├── images/
│   ├── weekly_demand_trend.png
│   └── material_shortage_analysis.png
├── outputs/
│   ├── demand_forecast.csv
│   └── material_requirements_plan.csv
└── README.md
```

*The structure above is the intended repository layout. Include only files that have actually been created and exported.*

## 11. How to Explore the Project

1. Clone or download this repository.
2. Open `Sumal_Q4_2026_Production_Planning.ipynb` in Jupyter Notebook or JupyterLab.
3. Install the required Python libraries in the active notebook environment.
4. Run the completed cells in order to reproduce the demand and material planning analysis.
5. Review the notebook outputs and visualizations, then follow the documented development of the optimization module.

## Author

**Adekunle Samuel Ojo**

Industrial and Production Engineering | Manufacturing and Operations Analytics

- LinkedIn: https://www.linkedin.com/in/adekunle-samuel-ojo/
- GitHub: https://github.com/AdekunleOjo
