# Sales insight Project - AtliQ Hardware![Screenshot 2023-12-05 120540](https://github.com/pranayshind/Sales_insight_Project/assets/143169584/b9eff8dc-7819-4259-b057-d6fb7071ff34)
# Problem statement:
In this project performed India based AtliQ hardware company sales insights - A Data Analysis project.
AtliQ Hardware is a company which supplies computer hardware and peripherals to many of clients such as surge stores, Nomad stores etc. across India. AtliQ Hardware head office is situated in Delhi, India and they have many regional office through out the India.
Sales director for this company is facing a lot of challenges is this the market is growing dynamically and sales director is facing issue in terms of tracking the sales in this dynamical growth market and he is having issues with growth of this bussiness, as overall sales was declining. He has regional manager for North India, South and Central India. Whenever he wants to get insights of thses region he would call these people and on the phone regional manager give some insights to him that this was the sales last quarter and we are going to grow by this much in the next quarter.
The problem was that all thses thing happening is verbal and these was mo proof with facts that how his business is affected and which made him frustraed as he can see that overall sales is declining but when he can ask regional manager, he is not getting complete picture of this bussiness and when he and this AtliQ hardware is big business. so to see insights clearly. and he will get proper insights anbd can take data driven decision to increase sales of hos company. All he wants is a simple data visualization tool which he can access on daily basis. By using such tools and technology one can make data driven decisiions which helps to increase the sales of the company. So, In this projects we will help a company make its own sales related dashboard using power BI.


# Data Analysis using MySQL:
Completed the Data discovery and then used mySQL for data analysis.
SQL database dump is in db_dump.sql file above. Download db_dump.sql file to your local computer


1.To find of all customers records

`SELECT * FROM sales.customers;`![sql1](https://github.com/pranayshind/Sales_insight_Project/assets/143169584/0047de40-9b97-4ce9-b8ba-228f56ab6557)


2.To find total number of customers

`SELECT count(*) From sales.customers;`

3.To find transactions for Chennai market (market code for chennai is Mark001

`SELECT * FROM sales.transactions where market_code='Mark001';`

4.To find distrinct product codes that were sold in chennai

`SELECT distinct product_code FROM sales.transactions where market_code='Mark001';`

5.To find transactions for Chennai market (market code for chennai is Mark002

`SELECT * FROM sales.transactions where market_code='Mark002';`

6.To find distrinct product codes that were sold in mumbai

`SELECT distinct product_code FROM sales.transactions where market_code='Mark002';`

7.To find transactions where currency is US dollars

`SELECT * from sales.transactions where currency="USD";`

8.To find transactions in 2020 join by date table

`SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020;`

8.To find transactions in 2019 join by date table

`SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2019;`

9.To find total revenue in year 2020,

`SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r";`

10.To find total revenue in year 2019,

`SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2019 and sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r";`

11.To find total revenue in year 2020, January Month,

`SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="January" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");`

12.To find total revenue in year 2020, February Month,

`SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="February" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");`

13.To find total revenue in year 2019, January Month,

`SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="January" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");`

14.To find total revenue in year 2019, February Month,

`SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="February" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");`

15.To find total revenue in year 2020 in Chennai

`SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.market_code="Mark001";`

16.To find total revenue in year 2020 in Mumbai

`SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.market_code="Mark002";`

Similarly, if we want different of any other particular city the market code of that city is used on the mysql workbench.

# Data Cleaning and ETL (Extract, Transform, Load):

In this process, we are work on data cleaning and ETL.

Step 1: Connect the MySQL database with the PowerBI desktop.

Step 2: Loading data into the Power BI deskstop. This step load all the tables and created in the data base. This load option will connect with the SQL and pull all the records into power BI environment.

Setp 3: Transform data with the help of Power Query

Perform filtration in market’s table: In the tables perform when we click on the transform data option, we are directed to Power query editor. Power query editor is where we perform out ETL.and then we can perform data transformation i.e. Data Cleaning, Data Wrangling, Data Munging. we need to filter the rows where the values are null and filtering the data and deselecting the blank option.

Perform filtration in Transaction’s table: In the table perform when we check the query in the MySQL to filter some negative values and also 0 values that appears in the table, the desired output is received.and we will perform the similar filtration in PowerBI. we have deselecting the values, don’t want in the table. The result after filtration. the zero values represent some garbage values which is not possible so we need to clean that data.

Convert USD into INR in the transaction’s table: the AtliQ Hardware only works in India so the USD values are not possible. we need to convert those USD values into INR by using some formulas. Add new column - Conditional column - normalized currency where sales amount will be in INR

In power query editore finding the total values having USD as currency.
 
 `=Table.AddColumn(#"Filtered Rows", "norm_sales_amount",each if [currency] = "USD" then [sales_amount]*75 else [sales_amount]`

 using this correct formula of the conversion,and converted the USD currency into INR.

# Data Modeling:
And then dataset was cleaned and transformed, it was ready to the data modeled.

The sales insights data tables as show below:
![powerbi](https://github.com/pranayshind/Sales_insight_Project/assets/143169584/ab811da7-8077-49b5-a4ac-383597c9e2f7)

# Build Dashboard Or a Report:
Data visualization for the data analysis (DAX) was done in Microsoft Power BI Desktop:

Shows visualizations from Sales insights :
![Screenshot 2023-12-05 120540](https://github.com/pranayshind/Sales_insight_Project/assets/143169584/c8fdfff5-ab0d-49e7-b43f-2898a162aa01)
![Delhi_Revenue](https://github.com/pranayshind/Sales_insight_Project/assets/143169584/cc423dbf-2d3f-4096-a9f6-1325cd7769eb)
![Mumabi revenue](https://github.com/pranayshind/Sales_insight_Project/assets/143169584/f06634b2-3d69-4700-afd6-d2e6a7e0131e)
![Ahemadabad](https://github.com/pranayshind/Sales_insight_Project/assets/143169584/8d83cd0f-44ed-4ce4-850e-0f6aa59cd46a)
