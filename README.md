# E-Commerce Data Cleaning & ETL Automation (GIFT 1 Case Study)

This project demonstrates an end-to-end data cleaning, transformation, and validation pipeline built in **Microsoft Excel Power Query (M Language)**. Using real-world e-commerce sales datasets containing severe data quality issues (such as mixed date formats, invalid currency symbols, negative quantities, and orphaned records), a structured, repeatable ETL process was developed to produce analysis-ready tables.

---

##  Project Overview

Real-world datasets are rarely analysis-ready. This case study focuses on handling dirty data using automated Power Query transformations, ensuring data integrity, correct relationships, and accurate business logic.

### Datasets Included
* **`Messy_List_of_Orders.csv`**: Contains order headers with customer and location details (~508 rows).
* **`Messy_Order_Details.csv`**: Contains line-item sales, quantities, and profit details (~1,506 rows).
* **`Messy_Sales_Target.csv`**: Contains monthly sales targets by product category (~44 rows).

---

##  Tools & Technologies Used
* **Microsoft Excel**: Power Query (ETL engine & M code), Data Modeling
* **Data Sources**: CSV Files

---

##  Key Cleaning & Transformation Steps

### 1. `Messy_List_of_Orders.csv`
* **Removed Irrelevant Columns**: Dropped `Notes` and `Sales_Rep` columns.
* **Handled Blank & Null Rows**: Filtered out empty records and placeholders (`"N/A"`, `"TBD"`).
* **Text Normalization**: Trimmed leading/trailing whitespace and standardized casing to Proper Case across `CustomerName`, `State`, and `City`.
* **Fixed Inconsistent State Names**: Corrected common abbreviations and typos manually (e.g., `MP` $\rightarrow$ `Madhya Pradesh`, `Maharastra` $\rightarrow$ `Maharashtra`, `T.N.` $\rightarrow$ `Tamil Nadu`).
* **Standardized Date Formats**: Parsed inconsistent date structures (`DD-MM-YYYY`, `MM/DD/YYYY`, `YYYY-MM-DD`) into a unified `Date` type.
* **Deduplication**: Removed exact duplicate rows.
<img width="1920" height="1080" alt="Screenshot (132)" src="https://github.com/user-attachments/assets/5e583711-ff00-4b5a-9b26-b8231e40b210" />
Messy List of Orders

  
<img width="1920" height="1080" alt="Screenshot (129)" src="https://github.com/user-attachments/assets/39ea079f-bc21-4891-9f30-7a086c94a5b5" />

Cleaned List of Orders

---
### 2. `Messy_Order_Details.csv`
* **Cleaned `Amount` Column**: Removed currency symbols (`₹`, `INR`), handled comma decimals, and converted to `Decimal Number`.
* **Cleaned `Profit` Column**: Fixed accounting negative representations (`(1148.0)` $\rightarrow$ `-1148.0`), stripped `%` signs, and set data type to `Decimal Number`.
* **Corrected Data Entry Errors**: Applied the **Absolute Value** transformation to fix negative `Quantity` values.
* **Text & Category Standardization**:
  * Capitalized each word for `Category` and `Sub-Category`.
  * Corrected typos (e.g., `Elec.` $\rightarrow$ `Electronics`, `Hankerchief` $\rightarrow$ `Handkerchief`, `Saree` $\rightarrow$ `Sarees`).
* **Referential Integrity**: Filtered out line items missing an `Order ID`.
* **Calculated Custom Columns**:
  * **`Profit Status`**: Conditional column categorizing records as `Profitable` (Profit $\ge 0$) or `Loss` (Profit $< 0$).
  * **`Revenue Per Unit`**: Custom calculated column (`[Amount] / [Quantity]`), formatted to 2 decimal places.
   <img width="1920" height="1080" alt="Screenshot (133)" src="https://github.com/user-attachments/assets/26927794-3e32-4cb2-b682-67cce097664c" />

    <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d5cd73cb-efba-49be-a1b3-873aa7482efc" /> 
Cleaned Order Details


---
<img width="1920" height="1080" alt="Screenshot (152)" src="https://github.com/user-attachments/assets/9f533a05-6491-40ad-a8b2-4839c05369b3" />

Calculated Column categorizing records

<img width="1920" height="1080" alt="Screenshot (153)" src="https://github.com/user-attachments/assets/a01471f0-fcd8-4d70-862d-22d93d96d641" />

Revenue per unit in two decimal places



---
### 3. `Messy_Sales_Target.csv`
* **Removed Irrelevant Data**: Dropped the `Region` column and removed blank/placeholder rows (`"TBD"`, `"Pending"`).
* **Target Value Cleaning**: Removed currency symbols (`₹`, `Rs.`) and commas, converting targets to numeric types.
* **Month Normalization**: Standardized mixed date representations (e.g., `Apr-18`, `April 2018`, `4/2018`) to uniform start-of-month dates.
<img width="1920" height="1080" alt="Screenshot (134)" src="https://github.com/user-attachments/assets/2675c4f2-7c51-4870-b17b-82772df65f5e" />
Messy Sales Target


<img width="1920" height="1080" alt="Screenshot (131)" src="https://github.com/user-attachments/assets/138a5bed-83f3-4437-ad9c-e09eef68ec97" /> 
Cleaned sales Target

---

##  Data Modeling & Merging

1. **Merged Orders & Order Details**: Joined `Messy_List_of_Orders` with `Messy_Order_Details` on `Order ID` using a **Left Outer Join** to integrate transaction-level details with customer metadata.
2. **Aggregated Order Details**: Created a reference query (`Messy_Order_Details_Aggregated`) grouping by `Order ID` to calculate `Total Amount`, `Total Profit`, and `Total Items`.
<img 
4. **Matched Sales Targets with Actuals**: Merged monthly sales targets with actual performance metrics using a multi-column join key (**`Month`** + **`Category`**).
---



---
##  Quality Assurance & Validation Checks

* **Row Count & Integrity**: Verified that no valid order header records were lost during merges.
* **Data Type Validation**: Confirmed that all columns are set to appropriate data types (`Date`, `Decimal Number`, `Text`, `Int64`).
* **Duplicate & Null Checks**: Re-verified key fields (`Order ID`) to ensure zero unlinked line items or unresolved duplicates.

---

##  Final Deliverable
The resulting dataset was loaded into **Microsoft Excel**, structured as production-ready, clean tables ready for PivotTable analysis, dashboard creation, and executive reporting.


---

##  About me
I am an emerging Data Analyst focused on building practical, real-world Business Intelligence solutions. I leverage Excel (Power Query & M Code), SQL, Power BI, and Python to transform messy datasets into automated ETL pipelines, clean relational models, and clear business insights. I am actively expanding my skill set by tackling end-to-end case studies and data engineering challenges.

*  **Linkedin**: https://www.linkedin.com/in/tamilore-tolulope-ajayi-44560a208/?isSelfProfile=true
*  **Project**: E-Commerce Sales Data Cleaning & Pipeline Automation (GIFT 1 Case Study)
*  **Core Tools**: Excel (Power Query & M Code), SQL, Power BI, Python
