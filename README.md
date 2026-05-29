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

### Data Modelling
The source data was a single flat Excel file (Sales_Data_2024.xlsx) containing all transactional records — sales and returns combined — across products, branches, payment methods, and customer types. A staging query (staging_Sales) was created in Power Query as the single source of truth, from which all dimension tables were derived. This approach ensures any change to the source file automatically propagates across the entire model.
Rather than using the flat file directly, a proper star schema was engineered entirely within Power Query — separating the data into one fact table and four dimension tables:
| Table         | Type          | Description   |
| ------------- | ------------- | ------------- |
| fact_Sales    | Fact          | Core transaction table — sales and returns with foreign keys  |
| dim_Product   | Dimension     | Product name and category  |
| dim_Branch    | Dimension     | Branch names  |
| dim_PaymentMethod  | Dimension  | Payment method and payment mode (Cash/Digital)  |
| dim_date      | Dimension     | Calender table  |

**How dimension tables were built:**
Each dimension table was derived from staging_Sales using a consistent pattern:
* Selected only the relevant columns
* Removed duplicates to get unique dimension values
* Added a surrogate key using an index column with formatted prefixes (e.g. PRD001, BRN001, PAY001)
* Applied correct data types

**How the fact table was built:**
The fact table was engineered by:
* Generating a Date Key in yyyyMMdd format
* Performing nested joins against each dimension table to bring in surrogate keys
* Removing the original text columns (Product Name, Category, Branch, Payment Method) - keeping only foreign keys in the fact table
* Applied correct data types

**Date Table**
A custom calendar table was built programmatically in Power Query - generating every date in 2024 from January 1 to December 31 - which includes :
* Date Key - yyyyMMdd format for joining to the fact table
* Month - numeric month (hidden, used for sort order)
* Month Name - full month name, sorted by the numeric Month column to ensure correct chronological order in visuals
* Quarter - "Quarter 1" through "Quarter 4"

The table was marked as a Date Table enabling official functions in DAX.
<img width="1000" height="500" alt="image" src="https://github.com/user-attachments/assets/2d42ba63-4bc6-45f8-8035-f4c2fad0d1c5" />

### Report Development
With the help of DAX, core metrics like gross sales, net sales, returns and return % were calculated. Dynamic KPI card measures were built to get a quick insight on the top category, top product, and most returned product responsively based on slicer context. Month-over-Month growth % allows the user to understand the direction and trend of the sales when compared month to month. The final report consists of two pages — a Sales Performance Dashboard and a Returns Analysis Dashboard — giving business users a self-serve tool to instantly monitor revenue trends, identify high-return products, compare branch performance, and analyse customer and payment behaviour through interactive slicers and drill-downs.

<img width="500" height="500" alt="Sales" src="https://github.com/user-attachments/assets/807fdbd8-b420-4c1d-ac39-dbcf16ab7135" />

<img width="500" height="500" alt="Sales Return" src="https://github.com/user-attachments/assets/8f545b98-d75e-4e0c-8746-0792ee0759c7" />

