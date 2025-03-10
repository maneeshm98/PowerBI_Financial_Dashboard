# PowerBI_Financial_Dashboard
Credit Card Financial Dashboards using Power BI and MySQL
# Credit Card Weekly Dashboard - README

## Project Objective
To develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends, enabling stakeholders to monitor and analyze credit card operations effectively.

---

## 1. Import Data to SQL Database
### Steps:
1. **Prepare CSV Files**
   - Export relevant credit card transaction data into CSV format.
2. **Create Tables in SQL**
   - Define table structures in SQL to store customer and transaction details.
3. **Import CSV Files into SQL**
   - Use SQL queries or bulk import tools to load data into tables.

---

## 2. Data Processing & DAX Queries

### Data Transformation using DAX

#### Categorizing Age Group:
```DAX
AgeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[customer_age] < 30, "20-30",
 'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
 'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
 'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
 'public cust_detail'[customer_age] >= 60, "60+",
 "unknown"
)
```

#### Categorizing Income Group:
```DAX
IncomeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[income] < 35000, "Low",
 'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Med",
 'public cust_detail'[income] >= 70000, "High",
 "unknown"
)
```

#### Revenue Calculation:
```DAX
Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
```

#### Week Number Calculation:
```DAX
week_num2 = WEEKNUM('public cc_detail'[week_start_date])
```

#### Current Week Revenue:
```DAX
Current_week_Reveneue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
 ALL('public cc_detail'),
 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
 ))
```

#### Previous Week Revenue:
```DAX
Previous_week_Reveneue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
 ALL('public cc_detail'),
 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1
 ))
```

---

## 3. Dashboard & Insights

### Key Metrics Visualized:
- **Revenue Trends**: Week-over-week revenue fluctuations.
- **Customer Segmentation**: Age group & income group classification.
- **Delinquency Rate**: Percentage of accounts with missed payments.
- **Card Category Performance**: Revenue & interest earnings by card type.
- **Customer Satisfaction**: Average satisfaction score & trends.

### Dashboard Implementation:
- Developed interactive Power BI visualizations.
- Utilized slicers for filtering data dynamically.
- Incorporated KPI cards for quick performance overview.

---

## 4. Export & Share Project
### Steps:
1. **Export Dashboard**
   - Saved Power BI report as .pbix file.
   - Exported key insights as CSV files.
2. **Sharing & Deployment**
   - Published the Power BI dashboard for stakeholder access.
   - Uploaded datasets and documentation to GitHub for reproducibility.

---

## Conclusion
This project successfully implemented a dynamic Power BI dashboard to analyze credit card transactions. The insights help stakeholders make informed decisions, improve customer targeting, and optimize financial performance.

