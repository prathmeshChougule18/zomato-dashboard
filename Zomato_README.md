# 🍽️ Zomato Sales & Performance Dashboard (Power BI)

An interactive Power BI dashboard analyzing Zomato's sales, user behaviour, and city-level performance metrics to drive data-informed business decisions.

---

## 📸 Dashboard Preview

> 📌 *Add screenshot of your dashboard here*

---

## 📁 Project Structure

```
zomato-dashboard/
├── Zomato_Dashboard.pbix    ← Power BI Dashboard file
└── README.md
```

---

## 📊 Dashboard Pages

### 1. 🏠 Index Page
- Navigation hub to all other pages
- Clean landing page with quick access buttons

---

### 2. 📈 Overview Page
Key business metrics and sales performance at a glance.

**KPI Cards:**
- Total Sale Value
- Total Orders
- Total Ratings Count
- Dynamic KPI comparisons (current vs previous period)

**Visuals:**
| Visual | Description |
|---|---|
| Line Chart | Sale Value trend over Years |
| Clustered Bar Chart | Top N Cities by Sales (dynamic TopN filter) |
| Slicers | Food Type filter (Veg/Non-Veg), City search, Rank Type |
| Multiple KPI Cards | Sale Value, Rating Count breakdowns |

---

### 3. 👤 User Performance Page
Deep dive into customer behaviour and retention analysis.

**KPI Cards:**
- Total User Count
- Active Users
- Gained Customers
- Lost Customers
- Total Ratings & Orders

**Visuals:**
| Visual | Description |
|---|---|
| Clustered Column Chart | User Count by Age group |
| Bar Chart | Gained Customers by Gender |
| Bar Chart | Lost Customers by Gender |
| Slicers | Food Type, City search |

---

### 4. 🏙️ City Performance Page
Granular performance analysis across all cities.

**KPI Cards:**
- Sale Value
- Rating Count
- Order Count

**Visuals:**
| Visual | Description |
|---|---|
| Clustered Bar Chart | Sale Value by City |
| Clustered Bar Chart | Rating Count by City |
| Clustered Bar Chart | Active Users by City |
| Detailed Table | City-wise Sales, Orders, Gained & Lost Customers |
| Slicers | Food Type, City filters |

---

## 📐 Data Model

| Table | Key Columns |
|---|---|
| `orders` | city, Type, Year, Rating_Count, Order_Count |
| `users` | Age, Gender |
| `Measure_Table` | Sale_Value, UserCount, ActiveUser, GainCustomers, LostCustomers, TopN_Sale, Dynamic_subHeading |
| `RankTable` | Type |

---

## 🔑 Key DAX Measures

```dax
-- Sale Value
Sale_Value = SUM(orders[sale_value])

-- Active Users
ActiveUser = DISTINCTCOUNT(orders[user_id])

-- Gained Customers (new users in current period)
GainCustomers = 
VAR CurrentUsers = VALUES(orders[user_id])
VAR PrevUsers = CALCULATETABLE(VALUES(orders[user_id]), PREVIOUSYEAR(...))
RETURN COUNTROWS(EXCEPT(CurrentUsers, PrevUsers))

-- Lost Customers
LostCustomers = 
VAR CurrentUsers = VALUES(orders[user_id])
VAR PrevUsers = CALCULATETABLE(VALUES(orders[user_id]), PREVIOUSYEAR(...))
RETURN COUNTROWS(EXCEPT(PrevUsers, CurrentUsers))

-- Dynamic TopN Cities
TopN_Sale = 
CALCULATE([Sale_Value],
    TOPN(SELECTEDVALUE(RankTable[Type]), ALL(orders[city]), [Sale_Value]))
```

---

## 💡 Key Business Insights

- 📍 **City-wise performance** — Identifies top revenue-generating cities and compares active users
- 📉 **Customer retention** — Tracks gained vs lost customers segmented by gender
- 👥 **User demographics** — Age-group distribution helps target marketing campaigns
- 📊 **Food type trends** — Veg vs Non-Veg sales comparison across cities
- 🏆 **Dynamic TopN** — Flexible ranking to view top 5/10/20 cities on demand

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| `Power BI Desktop` | Dashboard development |
| `DAX` | Calculated measures & KPIs |
| `Power Query` | Data transformation & cleaning |
| `Data Modeling` | Table relationships & schema |

---

## ⚙️ How to Open

1. Download `Zomato_Dashboard.pbix`
2. Open with **Power BI Desktop** *(free download from Microsoft)*
3. Explore all 4 pages using the navigation buttons

> 💡 **Tip** — Use the food type slicer (Veg/Non-Veg) and city search to filter data across all pages simultaneously!

---

## 👨‍💻 Author

**Prathamesh Chougule**
- 🔗 GitHub: [@prathmeshChougule18](https://github.com/prathmeshChougule18)
- 💼 LinkedIn: [prathmesh-chougule](https://www.linkedin.com/in/prathmesh-chougule-7b8733219/)

---

© 2026 Prathamesh Chougule · All Rights Reserved
