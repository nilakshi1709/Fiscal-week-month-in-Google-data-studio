# Fiscal-week-month-in-Google-data-studio
How to have the custom time dimensions as Fiscal week and month in Google Data Studio.

- Fiscal weeks and months don’t exist as a time dimension in Data Studio.

- To have the custom time dimension , we have to create view in BigQuery to join the data table with the [dim_date](https://drive.google.com/open?id=1X1OqY_XK_q3AFaSwB9y_XDSphMEB2IXa1wQE7jiRfx0) table 
   ( which contains fiscal week, fiscal month, fiscal quarter, fiscal year).
- Then you can actually add the join tables in the Google Data Studio to have custom time dimension.

#### Steps Involved :
1. Create view in BigQuery to join data table with dim date table.
   Google analytics data is joined with dim date 454 in below example:
   ```
   SELECT
      date,
      fiscal_week_start_date,
      fiscal_month_start_date,
      fiscal_quarter_start_date,
      fiscal_year_start_date,
      sum(revenue) as sales,
      sum(transactions) as orders,
      sum(sessions) as visits From `project.dataset.table` as a join dim_date_454` as b on a.date=(b.date_value)
      group by 1,2,3,4,5
     ```
2. Add the Table created in step1 to data studio
   - Click on add new data source
   - Select BigQuery connector
   - Select Table
   - Click on connect at the top right corner of the screen and add the table to the report
   
3. Add the scorecard to report and select metric as below:
![alt text](https://drive.google.com/uc?id=1TKkOXQSLWCQC7QD021exXUxFLXRuWXOI)

4. Add "Filter control" to the report and select “fiscal_week_start_date” or “fiscal_month_start_date”  as Dimension
![alt text](https://drive.google.com/uc?id=1hgRSJhhDn3h5hu-Ml1_WP1U7jvn9Nyh-)

5. Click on View

![alt text](https://drive.google.com/uc?id=1XUPUC11TuSxSokgVBO4Aq-_elXkeMixk)

6. Select required fiscal week from the drop down 

 ![alt text](https://drive.google.com/uc?id=1XheaII16JUVzbfcxl2nE6vmc821RS34a)

7. Get the final report by fiscal week as below:

![alt text](https://drive.google.com/uc?id=1gzPlz2KTE-zKU5Ge8eGYrG4_bp8ryRgA)

8. Follow the similar process for fiscal month.
