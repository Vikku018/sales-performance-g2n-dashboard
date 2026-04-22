# 🍃 Green Beverages — Power BI Dashboard
### DataRoars Assignment | Sales & Revenue Analytics

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Measures-green?style=for-the-badge)
![Excel](https://img.shields.io/badge/Excel-Data%20Model-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)



---

## 📊 Dashboard Pages

### Page 1 — Financial Report (Tea Category)
- Vol in Kg & H_Tonnes
- Net Revenue & G2N per Kg
- Major Sourcing, Category, Vs PY NR%
- Sunburst / Donut chart by Grade → Customer Type → Trade Type
- Default filter: **Tea category**

### Page 2 — Sales Overview
- Net Revenue $MM, Total Bills, Total Customers
- Salesman Experience gauge
- World map by customer city
- Treemap by product (color: green→red by value)
- Customer Type donut
- Product Category Volume bar chart

### Page 3 — NR Analysis *(Most Critical)*
- Year/Month matrix with NR, YTD, PY NR, vs PY NR, vs PY%
- Month/Quarter/Year/Day slicers
- KPI cards: NR Share%, Vs PY NR%, Discount%
- Daily line chart: Net Revenue vs PY Net Revenue

---

## 🗃️ Data Model

| Table | Description |
|-------|-------------|
| Sales | Transactions (81,432 rows) |
| Product | 20 products with Unit to Kg conversion |
| Customer | 55 customers with Grade |
| Customer Grade | Discount % by grade |
| Area | Region/City mapping |
| Beat | Salesperson territory |
| Sales Person | Name, Age, Experience |
| **Calendar** | Created in Power BI (2018–2020) |

---

## 🧮 Key DAX Measures

### Volume
```dax
Vol Kg = SUMX(Sales, Sales[Vol] / RELATED(Product[Unit to Kg]))
Vol h_Tonnes = [Vol Kg] / 100000
```

### G2N Components
```dax
Net Revenue = 
    [Gross Sales] - [Resizing] + [Tax Incentives] 
    - [Free Goods] - [Cut-off] + [Royalty] 
    - [Customer Grade Discount]

G2N = [Gross Sales] - [Net Revenue]
```

### Time Intelligence
```dax
NR PY     = CALCULATE([Net Revenue], SAMEPERIODLASTYEAR('Calendar'[Date]))
NR YTD    = TOTALYTD([Net Revenue], 'Calendar'[Date])
vs PY NR% = DIVIDE([Net Revenue] - [NR PY], [Net Revenue])  -- divide by CY
```

### Page 3 KPIs
```dax
NR Share%  = DIVIDE([Net Revenue], CALCULATE([Net Revenue], ALL('Calendar'), ALL(Sales)))
Discount%  = DIVIDE([Customer Grade Discount], [Gross Sales])
```

---

## 📐 G2N Logic

| Component | Rule |
|-----------|------|
| Resizing | PRDT-11 = $5/kg, PRDT-13 = $7/kg |
| Tax Incentives | Frozen=$10, Kitchen=$12, Supplements=$5 (per kg) |
| Free Goods | Grade C=$2, D=$4, G in Jan/Aug=$2.5 (per kg) |
| Cut-off | North+202001=$5, West+201911=$3.5 (per kg) |
| Royalty | Retail Chain + Chocolate = $2/kg |
| Grade Discount | Vol_Kg × Price/kg × Discount% from Customer Grade table |

---

## ✅ Verified Numbers

| Metric | Value |
|--------|-------|
| Total Gross Revenue | $16.1B |
| Total Net Revenue | $15.5B |
| Total G2N | $617.8M |
| NR 2018 | $5,164M |
| NR 2019 | $4,956M |
| NR 2020 | $5,400M |
| Vs PY NR% (2020) | 8.22% |
| Discount% | 5.00% |

---

## 🗂️ Files

```
├── All_data.xlsx          # Source data
├── GreenBeverages.pbix    # Power BI report
└── README.md
```

---

## 🛠️ Setup

1. Open `GreenBeverages.pbix` in Power BI Desktop
2. If data missing → Transform Data → update source path to `All_data.xlsx`
3. Refresh data
4. All measures auto-calculate ✅

---

## 📌 Notes

- All prices in **USD** (ignore any "Rs." display)
- vs PY NR% divides by **current year** (not prior year)
- NR Share% is **non-dynamic** — uses `ALL()` to ignore filters
- Calendar table **required** for all time intelligence functions
- Sunburst replaced with Donut chart (permitted per assignment)

---

## 👤 About
Built by Vikku Kumar
Role: Power BI Developer | Data Analyst
LinkedIn: [[your link]](https://www.linkedin.com/in/vikku-kumar/)
Email: vikku.kr98@gmail.com
