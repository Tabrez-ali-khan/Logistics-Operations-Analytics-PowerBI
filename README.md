# Logistics Operations Analytics Dashboard | Power BI

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-8E44AD?style=for-the-badge)
![Power Query](https://img.shields.io/badge/Power_Query-217346?style=for-the-badge)
![Excel](https://img.shields.io/badge/Excel-1F4E79?style=for-the-badge&logo=microsoftexcel&logoColor=white)

A four-page Power BI report for a UK delivery network, built from a written business requirements document. It tracks orders, on-time delivery, customer satisfaction and delivery time, then breaks performance down by **hub, driver and vehicle** across **27,979 orders from January 2023 to December 2024**.

<img width="1576" height="917" alt="Image" src="https://github.com/user-attachments/assets/840882f5-99d1-4bb8-8732-7e3792e91d10" />

> **About the data:** this project uses a **randomly generated (synthetic) dataset** created for practice. It does not represent a real logistics company, drivers or vehicles. The findings illustrate the method and are not real business results.

---

## Project at a Glance

| Metric | Value |
| --- | --- |
| Orders | 27,979 (13,976 in 2023 and 14,003 in 2024) |
| Period | 1 Jan 2023 – 31 Dec 2024 |
| Hubs / drivers / vehicles | 6 / 55 / 45 |
| On-time orders | 78.9% (22,071 orders) |
| Average delivery time | 35.8 hours |
| Average hub processing time | 2.0 hours |
| Average customer rating | 4.17 out of 5 (84% of orders rated 4 or 5) |
| Cancelled orders | 252 (0.9%) |

---

## Business Questions

1. How many orders are handled each month, and how do on-time delivery, satisfaction and delivery time change from the previous month?
2. Which hubs handle the most orders, and how do they compare on capacity and on-time performance?
3. Which drivers are delayed most often, and does experience or rating explain it?
4. Which vehicles and vehicle models break down most, and does vehicle age matter?
5. What causes delays?

---

## Tools

Power BI Desktop · DAX · Power Query · Data Modelling · Time Intelligence · Microsoft Excel (source data)

---

## Dataset

The data is in the [`data/`][Drivers.xlsx](https://github.com/user-attachments/files/33028077/Drivers.xlsx)
[Hubs.xlsx](https://github.com/user-attachments/files/33028076/Hubs.xlsx)
[Orders.xlsx](https://github.com/user-attachments/files/33028074/Orders.xlsx)
[Vehicles.xlsx](https://github.com/user-attachments/files/33028075/Vehicles.xlsx) folder, in four Excel files.

| File | Rows | Contents |
| --- | --- | --- |
| `Orders.xlsx` (fact) | 27,979 | Order date, actual delivery date, hub, driver, vehicle, on-time and delayed flags, delay reason, order status, delivery time (hours), hub processing time (hours), customer satisfaction score (1 to 5) |
| `Drivers.xlsx` | 55 | Driver name, employment type, hire date, years of experience, performance rating (1 to 5) |
| `Hubs.xlsx` | 6 | Hub name and hub capacity |
| `Vehicles.xlsx` | 45 | Vehicle code, model, type, status, purchase date, breakdown count, maintenance alert |

The report also uses a **Date Table** and a **Select Measure** table, which powers the measure selector on the Drivers page. The business requirements are in [`docs/Business_Requirements.docx`][Business_Requirements.docx](https://github.com/user-attachments/files/33028135/Business_Requirements.docx).

---

## Approach

### 1. Requirements first
Started from a business requirements document that lists every KPI, chart type and business use case for each page, then built the report to match it.

### 2. Data preparation and model
- Loaded and shaped the four source tables with **Power Query**
- Built a model with `Orders` as the fact table and `Drivers`, `Hubs`, `Vehicles` and a `Date Table` as dimension tables
- Added a disconnected `Select Measure` table so users can switch the measure shown in a chart

### 3. DAX measures
Measures cover total orders, on-time delivery rate, delayed delivery rate, CSAT %, average delivery time, and the number of hubs, drivers and vehicles. The KPI cards also show the **previous month** and the **month-over-month change** for the selected year and month.

---

## Dashboard Pages

### 1. Overview
KPI cards for total orders, on-time delivery rate, CSAT % and average delivery time, each with previous month and MoM change, plus Year and Month slicers. Below them are hub, driver and vehicle summaries: orders vs hub capacity, hub ranking by on-time rate, experience vs rating, drivers with the most delays, active vehicles and orders by vehicle model.

### 2. Drivers Overview
Number of drivers, experience vs rating scatter plot, drivers with the most delays, a driver profile card (hire date, years of experience, star rating) driven by a driver-name slicer, and a monthly trend with a measure selector.

<img width="1572" height="915" alt="Image" src="https://github.com/user-attachments/assets/203768d1-4f4a-4fc7-bad1-a07b5b00de4e" />

### 3. Hubs Overview
Number of hubs, orders vs hub capacity, hub ranking, and average delivery time by hub, shown as a matrix by day, a column chart and a bar chart.

<img width="1576" height="921" alt="Image" src="https://github.com/user-attachments/assets/f660e1f5-d530-458c-b8fd-894c9bd963ed" />

### 4. Vehicles Overview
Number of vehicles, active vs in-maintenance donut, orders by vehicle model and type, vehicle age vs breakdowns scatter plot, and breakdowns by vehicle code and model, with vehicle type and status slicers.

<img width="1577" height="925" alt="Image" src="https://github.com/user-attachments/assets/1325c9b3-b67b-4a3d-96e4-0b4d2b704917" />

Every page has a page navigator and responds to the Year and Month slicers where they appear.

---

## Key Insights

**Orders and delivery**
- **Order volume is steady** at about 1,166 a month, between 1,036 and 1,233, with almost no growth from 2023 to 2024.
- **78.9% of orders were on time.** Monthly on-time rates ranged from 76.6% to 81.4%.
- **Delays have no single cause.** The 10 recorded reasons each account for roughly 9% to 11% of delayed orders, led by Roadworks and Vehicle Breakdown (623 each).
- All 252 cancelled orders carry the lowest satisfaction score of 1.

**Hubs**
- **Park Royal Main Hub (7,345 orders) and Heathrow Hub (6,875) handle about half of all orders.**
- **Hub on-time rates are close together,** from 77.9% at Croydon to 80.6% at Stratford, a gap of only 2.7 percentage points. The delay problem is network-wide rather than one weak hub.

**Drivers**
- **Delay rates range from 17.7% to 25.7% across the 55 drivers.** The highest are Archie Palmer (25.7%), Leo Barnes (24.8%) and Tara Singh (24.4%).
- **Rating does not predict punctuality.** About 21% of orders are delayed at every rating level from 1 to 5, so rating alone is a poor guide for coaching.
- Experience and rating are positively related (correlation 0.45).

**Vehicles**
- **Older vehicles break down more.** Vehicle age and breakdowns have a correlation of 0.65, measured as of 31 Dec 2024.
- **The DAF LF averages 17 breakdowns per vehicle** across 9 vehicles, 153 of the fleet's 537 breakdowns (28.5%). The Vauxhall Movano averages 5.5.
- **Lorries average 14.0 breakdowns against 10.3 for vans.** The 12 vehicles in maintenance average 15.6 breakdowns against 10.6 for active vehicles.

---

## Recommendations

- **Review the DAF LF fleet and the oldest vehicles first** for replacement or heavier maintenance, since they drive a large share of breakdowns.
- **Coach drivers on delay rate, not rating.** Start with the three drivers above 24%.
- **Target the top delay reasons together:** route planning for Roadworks and preventive maintenance for Vehicle Breakdown.
- **Look at network-wide fixes** such as hub processing and sorting errors, since no hub stands out.
- **Track the on-time rate monthly** against the 76.6% to 81.4% range seen here to spot real changes.

---

## Limitations

- The data is synthetic, so the findings illustrate the method and are not real business results.
- The source data flags the 252 cancelled orders as delayed, so the delayed share includes them.
- Hub capacity has no stated unit in the source data, so the orders vs capacity chart shows relative size only.
- Relationships such as age vs breakdowns are correlations in a small fleet of 45 vehicles and do not prove cause.
- The data covers two years and has no cost or revenue fields.

---

## Repository Structure

```
Logistics-Operations-Analytics-PowerBI/
├── README.md
├── data/
│   ├── Orders.xlsx
│   ├── Drivers.xlsx
│   ├── Hubs.xlsx
│   └── Vehicles.xlsx
├── docs/
│   └── Business_Requirements.docx
├── powerbi/
│   └── Logistics_Dashboard.pbix
└── screenshots/
    ├── 01_Overview.png
    ├── 02_Drivers_Overview.png
    ├── 03_Hubs_Overview.png
    └── 04_Vehicles_Overview.png
```

## Run It Yourself

1. Download `Logistics_Dashboard.pbix` from the `powerbi/` folder and open it in **Power BI Desktop**.
2. Use the Year and Month slicers, and the page navigator, to move around the report.
3. If Power BI asks for the data source path, go to **Transform data → Data source settings → Change Source** and point each table to the matching file in `data/`.

---

## Author

**Mohammed Tabrez Ali Khan** · Data Analyst
Riyadh, Saudi Arabia · [LinkedIn](https://www.linkedin.com/in/md-tabrez-ali-khan) · mdtabrezalik@gmail.com
