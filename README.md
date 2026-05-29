## Retail Sales and Returns Analysis Report 2024 | Power BI
An interactive Power BI report analyzing retail business performance, product sales and return behaviour, customer transaction patterns and payment 
trends.

### Problem Statement
A retail business operating across two branches — City Center and Riverside — needed clear visibility into:
* How sales are trending month over month
* Which products and categories are driving revenue
* Where returns are concentrated and why
* How different customer types and payment modes behave

The data was available in a flat Excel sheet.

### Data Model
Transformed the flat file into a star schema by splitting the data into fact and dimension tables using Power Query.
Quantitative data like sales, sales return, quantity, cost price were kept in the fact tables along with foreign key columns for joining them to the dimension tables. Business entities like product details, branch, payment method were splitted into different dimension tables along with primary key columns. Created date table for time intelligence calculations. Relationships were defined between fact and dimension tables. 
<img width="1300" height="700" alt="image" src="https://github.com/user-attachments/assets/2d42ba63-4bc6-45f8-8035-f4c2fad0d1c5" />

### Calculations & Report Development

