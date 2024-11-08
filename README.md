# LITA_Capstone_Project_SalesData
---
This where i want to analysis one of the projects for the completion of my Data analysis training with Incubator Hub

 ## Project Title: Performance Analysis for a Company
 ---
 
 [Project Overview](#project-overview)

[Data Sources](#data-sources)

[Tools Used](#tools-used)

[Data Cleaning and preparation](#data-cleaning-and-preparation)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)

[Findings](#finding)

[Conclusion](#conclusion)



 
 
## Project Overview
---
This project is geared towards analyzing  the sales performance of a company by exploring sales data to uncover insights such as top-selling products, regional performance, and monthly sales trends. The primary objective is to create an interactive Power BI dashboard that highlights key findings, enabling data-driven decision-making to improve sales strategies. The project involves data exploration, preparation, and analysis using Excel and SQL, with final visualizations in Power BI


## Data Sources:
---

The primary source of this data is HR DATA.excel provided by LITA and this is an open sources data that can freely downloaded without any restriction, online such as kaggle or fred, data.gov as well as any other sources like industry report.



## Tools Used:
 - Excel Microsoft Excel[Download Here](https://www.microsoft.com
     - For initial data exploration, 
     - creating pivot tables, 
       and calculating summary statistics using Average and 
 - SQL -Structured query language [Download Here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
     - For data extraction and analysis through structured queries.
 - Power BI - power business intellegence:[download Here](https://power-bi-desktop.en.microsoft.com)
     - For building an interactive dashboard to visualize key insights, trends, and segments.
 - Gitup- Github account[Download Here](https://www.github.com)
     - for portfolio building
  


 - 
  
 ## Data Cleaning and Preparation:
---
- Duplicates remover:
   - Check for duplicate rows in the dataset, especially in CustomerID or subscription records, and remove any redundancies.
   - Standardize Data:
   - Ensure consistency in data formats, such as dates (SubscriptionStart, SubscriptionEnd),
   - I checked for uniformity in categorical fields like SubscriptionType and Region.
   - Data Transformation: Calculate new fields, such as subscription duration   .
   - Active Status: Create an indicator for active subscriptions based on SubscriptionEnd and Canceled columns.
 
  ## Exploratory Data Analysis:

  - Retrieve the total sales for each product category. 
  - Find the number of sales transactions in each region. 
  - Find the highest-selling product by total sales value. 
  - Calculate total revenue per product. 
  - calculate monthly sales totals for the current year. 
  - find the top 5 customers by total purchase amount. 
  - calculate the percentage of total sales contributed by each region. 
  - identify products with no sales in the last quarter.
  ---
  

## Data Analysis:
---

```SQL
Create database Capstone_project

Select * from [dbo].[SalesData_PS]

---1.Total Sales for product Category---

Select Product, Sum(quantity*unitPrice) as TotalSales
from[dbo].[SalesData_PS]
group by product
order by TotalSales desc

Product	TotalSales
Shoes	613380
Shirt	485600
Hat	316195
Gloves	296900
Jacket	208230
Socks	180785
Above is summary of total Sales per Product



---2. Number of Sales transactions in each Region---

Select Region, count(OrderID) as Number_of_Sales
from[dbo].[SalesData_PS]
group by Region
order by Number_of_Sales desc

Region	Number_of_Sales
East	2483
North	2481
South	2480
West	2477

---3. The highest selling product by total sales value---

select Top 1 product,sum(quantity*unitPrice) as Total_sales_Value
from[dbo].[SalesData_PS]
group by Product

Product	Total_sales_Value
Shoes	613380



--4. Total Revenue by Product
Select Product, Sum(quantity*unitPrice) as TotalRevenue
from[dbo].[SalesData_PS]
group by product
order by TotalRevenue desc

Product	TotalRevenue
Shoes	613,380
Shirt	485,600
Hat	316,195
Gloves	296,900
Jacket	208,230
Socks	180,785
The Product with the highest sales is Shoes at the worth of 613,380



--5.Total Monthly Sales for 2024 (current year)

Select 
Case Month(orderdate)
when 1 then 'January'
when 2 then 'Febuary'
when 3 then 'March'
when 4 then 'April'
when 5 then 'May'
when 6 then 'June'
when 7 then 'July'
when 8 then 'August'
when 9 then 'September'
when 10 then 'October'
when 11 then 'November'
when 12 then 'December'
end as Month,
Sum(quantity*unitprice) as monthlysales
from [dbo].[SalesData_PS]
where Year(orderdate)= Year(getdate())
group by Month(orderdate)
order by Month(orderdate)

Month	monthlysales
January	198,400
Febuary	298,800
March   54,780
April	 9,440
May	 44,640
June	 148,200
July	 37,200
August	174,300

Monthly sales is as stated above, February has the highest performance with month sales of 298800


---6.TOP 5 CUSTOMERS BY TOTAL PURCHASE AMOUNT

Select top 5 Customer_Id, Sum(Quantity*UnitPrice) as Total_Purchase_Amount
from [dbo].[SalesData_PS]
group by Customer_Id
order by Total_Purchase_Amount desc

Customer_Id Total_Purchase_Amount

Cus1431    4235               
Cus1495    4235               
Cus1005    4235               
Cus1115    4235               
Cus1302    4235               

---7. % (PERCENTAGE) OF TOTAL SALES CONTRIBUTED BY EACH REGION---

Select Region,
Sum(quantity*unitprice) as Total_Sales,
Sum(quantity*unitprice)*100.0/(Select Sum(quantity*unitprice)
From [dbo].[SalesData_PS])
as Percentage_of_Totalsales
From [dbo].[SalesData_PS]
Group by Region
Order by percentage_of_totalsales desc
```

|Total_Sales|Region|Percentage_of_Totalsales|
|-----------|------|------------------------|
|#927,820   |South	|44%                     |
|#485925    |East |23%                     |
|#387,000	  |North |18%                     |
|#300,345	  |West  |14%                     |



```
---8 PRODUCT WITH NO SALES IN LAST QUARTER---
Select distinct product
From [dbo].[SalesData_PS]
Where product Not In(
Select product
From [dbo].[SalesData_PS]
Where OrderDate >= DateAdd(quarter, -1, GetDate()) and OrderDate < GetDate());

Product
Gloves
Jacket
Shirt
Shoes
Socks
```








## Data Visualization


![Power bi dashboard sales data](https://github.com/user-attachments/assets/eaa18494-624c-4320-9855-6f3a7f211c77)

## Findings
---

Conclusion:
---
