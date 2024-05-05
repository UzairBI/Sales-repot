# Sales-report
Design a comprehensive dashboard using Power BI to analyze sales data across various categories and perform trend analysis.
Supermarket Sales Dashboard using Power BI - Explanation
Objective: Design a comprehensive dashboard using Power BI to analyze sales data across various categories and perform trend analysis.
1. Data Collection:
Obtain sales data from relevant sources, ensuring it includes essential information such as sales data, gender, city, payment type, product line, gross income and ratings.

2. Data Cleaning and Transformation:
Cleanse the data to remove inconsistencies, handle values, and format data types appropriately. Transform the data as needed to facilitate analysis, such as extracting year and month from sales date.
	Formula: month(supermarketsales(date),”MMMM”)
Cleaned the error while transform the data type of date column by:
Formula: text.beforedelimiter(text.afterdelimiter([date],”/”), “/” ) & “/” &                           (text.beforedelimiter([date],”/”) & “/” & text.afterdemiliter((text.afterdelimiter([date],”/”), “/”)
Dashboard components:
1. Sales Data Categorized by Year:
Visualize total sales for each year using bar chart.
Enable users to drill down into specific years for deeper analysis.
Used slicer for better granularity.
Added dynamic titles using DAX function.
Created new Calendar Table in Data tab and marked as Date Table for analysis related on year, month. Managed the relationship between calendar table and sales table with 0ne-to-many in Modeling Tab. 

Formula: sum(supermarketsales[amount])
Formula: calendar(startdate,enddate) – Calendar Table
Formula: “total sales by ” & if(isfiltered(supermarketsales[date].[year], “year”, “month”)
2. Sales Data Categorized by Month:
Visualize total sales for each year using bar chart.
Enable users to drill down into specific month for deeper analysis.
Used slicer for better granularity.
Added dynamic titles using DAX function.

Formula : sum(supermarketsales[amount])

Formula: “total sales by ” & if(isfiltered(supermarketsales[date].[year], “year”, “month”)

3. Sales Data Categorized by Gender:
Illustrate total sales distribution by gender using a donut chart.
Provide insights into gender based purchasing behavior.
Used slicer for better granularity.
Added dynamic titles using DAX function.

           Formula: “total sales by ” & if(isfiltered(supermarketsales[gender]), selectedvalue(supermarketsales[gender]), “gender”)

4. Sales Data Categorized by City:
Showcase total sales across different cities using bar chart.
Enable users to interactively explore sales performance by location. Note: can’t use map visual due to unavailable of account.
Used slicer for better granularity.
Added dynamic titles using DAX function.
Formula: “total sales by ” & if(isfiltered(supermarketsales[city]), selectedvalue(supermarketsales[city]), “city”)

5. Sales Data Categorized by Payment Type:
Visualize the distribution of sales by payment method using pie chart.
Identify popular payment methods and their impact on overall sales.
Used slicer for better granularity.
Added dynamic titles using DAX function.

Formula for all type : calculate(count(supermarketsales[paymenttype]), supermarketsales[paymenttype] = “cash”)
Formula: “total sales by ” & if(isfiltered(supermarketsales[paymenttype]), selectedvalue(supermarketsales[paymenttype]), “paymenttype”)

6. Sales Data Categorized by Product Line, Including Gross Income:
Present total gross income for each product line using clustered line chart.
Highlight top-performing product lines and their contribution to revenue by conditional formatting.
Used slicer for better granularity.
Added dynamic titles using DAX function.

Formula: gross income = sum(supermarketsales[amount]) – sum(supermarketsales[cags])

Formula: “total sales by ” & if(isfiltered(supermarketsales[productline]), selectedvalue(supermarketsales[productline]), “productline”)


7. Trend Analysis of Sales over Time:
Visualize total sales trends over time using a line chart, grouped the time column for accurate analysis.
Include trend lines to highlight patterns and fluctuations.
Used stepped line format to visualize the pattern.

8. Average Ratings for Each Product Line:
Display average product ratings for each product line using area chart.
Evaluate customer satisfaction and product performance across different product lines.
Used slicer for better granularity.
Added dynamic titles using DAX function.

Formula: average(supermarketsales[ratings])

Formula: “total sales by ” & if(isfiltered(supermarketsales[productline]), selectedvalue(supermarketsales[productline]), “productline”)

Explanation:
This dashboard provides a comprehensive view of sales performance across various dimensions, enabling stakeholders to make informed decisions.
Utilizing Power BI's interactive features, users can drill down into specific categories for deeper analysis.
Trend analysis helps identify patterns and make future predictions, while average ratings offer insights into product performance.
The dashboard is designed for easy interpretation and action ability, empowering users to drive business growth effectively.

3. Interactive features:
Incorporate slicers for filtering data by year, month, gender, city, payment type, product line to enable interactive exploration.
Applied selection pane and bookmarks to hide and show slicer panel using icon action button.
Utilized drill-through functionality to allow users to navigate to detailed reports or data subsets for deeper analysis.
Added required measure details in Tool-Tip, to visualize the reports in depth.


4. Dashboard layout and Design:

Arrange visualizations in a logical and visually appealing layout on the dashboard canvas.
Ensure consistency in formatting, colors, fonts, and chart styles foe a potential look and feel.
Add titles, subtitles, and descriptions to provide context and guide users through the dashboard.

Formula for subtitle: format(sum(sales[amount]), #,##0,. 00 K )



5. Testing and Validation:
Thoroughly test the dashboard to ensure all visualizations are functioning correctly and providing accurate insights.
Validate data accuracy and consistency across different dimensions and filters. 


Insights and recommendations:

1. Sales Trends over Time:
Identify overall sales trends, including periods of growth, decline or seasonality.
Understand the impact of marketing campaigns, promotions, or external factors on sales.
Forecast future sales based on raw data. 

Note: After analysis, the time segment between 18.00-20.00 has most number of purchase and sales.
          Average sales of 15K Dollars using Average lines. Used Forecast lines too.

2. Sales Data Categorized by Year and Month:

Analyze Month over Month sales growth or decline.
Determine which month or year are performing best or worst I terms or sales.

Formula: var currentmonthsales = calculate(sum(sales[amount])
	Var previousmonthsales = calculate(sum(sales[amount]), previousmonth(calendar[date]) 
Return
	Divide (currentmonthsales – previousmonthsales, previousmonthsales,0)

Note: After analysis, the overall sales have reduced 16% in February. Next month march has 12% sales increase from February, but it’s not up to the mark has on January. Especially in home and lifestyle, sports and travel sales had reduced 39.33% and 36.26% in February. But in March it has increased to 68.35% and 48.26% which is interesting. It’s seems that start of holiday time.


3. Sales Data Categorized by Gender:
Understand purchasing behavior differences between male and female customers.
Tailor marketing strategies and product offerings to specific gender demographics.

Note: After analysis, male customers have purchase behavior of 48.02% and female customers have 51.98%.

4. Sales Data Categorized by City:
Identify top performing and underperforming cities using topN visual filter.
Allocate resources and marketing efforts to high-potential areas.
Identify geographical trends for expansion.

Note: After analysis, Naypyitaw city has most sales and Mandalay with low sales.

5. Sales Data Categorized by Payment type:
Determine the most popular payment among customers.
Optimize payment processing system based on customer preferences.
Identify the trend over time.

Note: After analysis, customers prefers to pay in Cash mostly, then Ewallet and Credit card.

6. Sales Data Categorized by Product line with gross income:
Identify top selling product lines and their contribution to overall revenue.
Determine which product lines are profitable.
Adjust inventory and marketing strategies based on performance. 
Note: After analysis, Food and Beverages have most of the sales and gross income and Health and Beauty have low sales and gross income. 
7. Average Ratings for each product line:
Evaluate customer satisfaction levels for different product lines.
Identify areas for product improvement.
Tailor marketing messaging based on customer feedback.

Note: After analysis, Food and Beverages have most average rating of 7.11 and Home and Lifestyle have 8.84.


Additional Insights:

Correlation analysis:
	Identify correlations between different variables.


Customer Segmentations:
	Segment the Product line based on the quantity purchasing behavior to tailor marketing efforts. Created separate segmentation table.

	Formula: summarize(sales, sales[product line], sales[time group] “segmentation”, [count of quantity])

Note: After analysis, customers placed orders on Fashion with most no.of count 178 than Food and Beverages  with 174. 


Anomaly Detection:
	Identify outliers in sales data that may require further investigation. 

Sales by Customer type:
	After analysis, customer type “Member” has contributed more in total sales of 50.85% .

Sales by Branches:
	After analysis, Branch ‘C’ has made more sales than ‘A’ and ‘B’ with 110K Dollars.

Note: created separate folder for all the Metrics in Modeling Tab.

					                 

  End of Analysis
