#  E-Commerce Sales Dashboard  
### Power BI Data Analytics Project  

##  Overview  
This Power BI dashboard provides an interactive overview of e-commerce sales performance, profitability, and return patterns.  
It helps business decision-makers track key metrics, analyze sales trends, and uncover actionable insights.

---

##  Objectives  
- Track **Total Sales**, **Profit**, and **Orders**  
- Measure **Return Rates** and identify inefficiencies  
- Compare performance across **regions** and **months**  
- Enable flexible filtering by **date**, **month**, and **region**

---

##  Data Model  
| **Table Name** | **Description** | **Key Columns** |
|-----------------|-----------------|-----------------|
| **Sales** | Order-level data including sales, profit, and quantities. | Order ID, Order Date, Sales, Profit |
| **Returns** | Records returned orders. | Order ID, ReturnedFlag |
| **People** | Contains sales reps or regional managers. | Person, Region |
| **Dates** | Calendar table for time intelligence. | Date, Year, MonthName |

Relationships established:  
- **Dates[Date] → Sales[Order Date]**  
- **People[Region] → Sales[Region]**

---

##  Key DAX Measures  
- **Total Sales** = `SUM(Sales[Sales])`  
- **Total Profit** = `SUM(Sales[Profit])`  
- **Total Orders** = `DISTINCTCOUNT(Sales[Order ID])`  
- **Returned Orders** = `CALCULATE(DISTINCTCOUNT(Sales[Order ID]), Sales[ReturnedFlag] = "Yes")`  
- **Return Rate** = `DIVIDE([Returned Orders], [Total Orders])`  
- **Sales LY** = `CALCULATE([Total Sales], SAMEPERIODLASTYEAR(Dates[Date]))`  
- **Sales YoY %** = `DIVIDE([Total Sales] - [Sales LY], [Sales LY])`  

---

##  Dashboard Visuals  
| **Visual** | **Purpose** |
|-------------|-------------|
|  **Total Sales & Profit Cards** | Displays KPIs at a glance |
|  **Total Orders Card** | Shows total number of unique orders |
|  **Return Rate Indicator** | Highlights % of returned orders |
|  **Sales Trend by Date (Line Chart)** | Tracks monthly or yearly sales |
|  **Sales by Region (Bar Chart)** | Compares regional performance |
|  **Top Products by Sales** | Identifies best-selling products |

---

##  Power Query Transformations  
1. **Merged Orders with Returns** on *Order ID* (Left Join).  
2. Expanded the `Returned` column → renamed as **ReturnedFlag**.  
3. Replaced nulls with `"No"`.  
4. Created a **Dates table** using DAX:  
   ```DAX
   Dates = CALENDAR( MIN(Sales[Order Date]), MAX(Sales[Order Date]) )
##  Insights

* The **West Region** generates the highest sales, followed by **East**.
* **Technology** and **Office Supplies** categories show consistent growth.
* **Sales peak** during **November and December**, aligning with holiday promotions.
* The **Return Rate** remains low, indicating strong customer satisfaction.
* **YoY growth** demonstrates steady business expansion.

---

##  Tools & Technologies

* **Microsoft Power BI Desktop** – Data modeling, visuals, and dashboard creation
* **Power Query** – Data cleaning, merging, and transformation
* **DAX (Data Analysis Expressions)** – Custom measures and KPIs
* **Excel / CSV Data Source** – Raw e-commerce datasets
* **Power BI Service (optional)** – Sharing and publishing dashboards online

---

##  How to Use

1. Open the provided **.pbit template** in Power BI Desktop.
2. When prompted, **connect to your Excel/CSV data sources**.
3. **Refresh the data model** to load your dataset.
4. Explore visuals using filters for **date**, **region**, and **category**.
5. **Customize** visuals or measures based on business needs.
6. *(Optional)* Publish to **Power BI Service** to share with your team.

---

##  Recommendations

* Add **forecasting visuals** to predict next-quarter sales.
* Integrate a **Profit Margin KPI** to highlight operational efficiency.
* Include **customer segmentation** to target repeat buyers.
* Automate **data refresh** using Power BI Gateway if deployed online.

---

##  Author

**Amanuel Tekalign**
Data Analyst
 [amanita4t@gmail.com]
