
# CHOCOLATE SALES ANALYSIS


## Problem Statement

- Analyse chocolate sales data by customer demographics, brand and product categories across diverse geographic locations. 

- Also, include the sales trends over various time periods throughout the year 2021. 

### Steps followed 

- Step 1 : Load the CSV files into MySQL, then connect MySQL to Power BI to load data into Power BI.
- Step 2 :Open the files into POWER QUERY EDITOR to clean the data, then click CLOSE & LOAD to load cleaned data. 
- Step 3 : Create a new table calender_dimension as shown below using the DAX query,

      calender_dimension = ADDCOLUMNS(CALENDAR(MIN('chocolate_project sales_fact_table'[Date]),
      MAX('chocolate_project sales_fact_table'[Date])),"YEAR",YEAR([Date]),"QUARTER","Q" & QUARTER([Date]),
      "MONTH",FORMAT([Date],"MMM"),"MONTH NUMBER",MONTH([Date]),"DAY",FORMAT([Date],"DDD"),"DAY NUMBER",WEEKDAY([Date]))

  ![image](https://github.com/user-attachments/assets/db6da8c1-f3ac-40f7-8d08-8c182be16076)

- Step 4 : Open the MODEL VIEW to make relationship among all the tables. The SCHEMA so formed is shown in the figure below. 
![image](https://github.com/user-attachments/assets/769feb2d-f2e6-4652-8594-d87a7c1801d2)

- Step 5 : Create a table named as 'Measure Table' to put all the DAX queries required for different measures. 
- Step 6 : Create a measure to find 'Change in Sales' using the DAX query. 
    
      Change_in_Sales =
       
      var previous_month_sales = CALCULATE([TotalSales],PARALLELPERIOD(calender_dimension[Date],-1,MONTH))

      var output = DIVIDE([TotalSales] - previous_month_sales,previous_month_sales)
            
      RETURN output
- Step 7 : Create a measure to find 'Festival Season Sales of last 3 months' using the DAX query. 

      Festival_Season_Sales(last3month) = CALCULATE([TotalSales],calender_dimension[MONTH NUMBER]= 10 ||
       calender_dimension[MONTH NUMBER] = 11 || calender_dimension[MONTH NUMBER]=12) 

- Step 8 : Create a measure to find 'Total Sales'  using the DAX query. 

      TotalSales = SUMX('chocolate_project sales_fact_table',
      'chocolate_project sales_fact_table'[Quantity_Sold]*RELATED('chocolate_project product_dimension'[Cost]))

- Step 9 : Create all the charts to Analyse 'Customer Demographics' as shown in the figure below.
  
  ![image](https://github.com/user-attachments/assets/1b587349-c5b7-44df-98e6-fe664f9edffe)

- Step 10 : Create all the charts to Analyse 'Sales Trends Over Time' as shown in the figure below.

  ![image](https://github.com/user-attachments/assets/32bbda26-b95d-49f6-b543-4a76dc167acd)

- Step 11 : Create all the charts to Analyse 'Product & Brand Statistics' as shown in the figure below.

  ![image](https://github.com/user-attachments/assets/d0af9ce9-25aa-4926-93b1-8008ae919c30)

- Step 12 : Create all the charts to Analyse 'Geographical Sales' as shown in the figure below.

  ![image](https://github.com/user-attachments/assets/8a8bdb07-acc4-4d13-96fa-1db0ff093feb)


- Step 13 : Create a final Sales Dashboard that offers a comprehensive 360-degree view of total sales, including insights into how sales are occurring across different dimensions such as city, gender, brand, and month. It should also include the overall sales value, the total quantity of chocolate sold, and identification of the leading brand and city in terms of sales.

  ![image](https://github.com/user-attachments/assets/15d06d10-4523-405a-958b-4ccba56cc7e9)

- Step 14 : Finally, make a report from all the charts to share with the client. 
