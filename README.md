
## BANK DATA ANALYSIS 

## Problem Statement:-

You are the database developer of an international bank. You are responsible for managing the bank’s database. You want to use the data to answer a few questions about your customers regarding withdrawal, deposit and so on, especially about the transaction amount on a particular date across various regions of the world. Perform SQL queries to get the key insights of a customer.

## Dataset:-
The 3 key datasets for this case study are:
- a. Continent: The Continent table has two attributes i.e., region_id and region_name, where region_name consists of different continents such as Asia, Europe, Africa etc., assigned with the unique region id.
- b. Customers: The Customers table has four attributes named customer_id, region_id, start_date and end_date which consists of 3500 records.
- c. Transaction: Finally, the Transaction table contains around 5850 records and has four attributes named customer_id, txn_date, txn_type and  txn_amount.
  The links of the datasets are available in csv format

## Tasks Performed:- 
1. Display the count of customers in each region who have done the transaction in the year 2020.
2. Display the maximum and minimum transaction amount of each transaction type.
3. Display the customer id, region name and transaction amount where transaction type is deposit and transaction amount > 2000.
4. Find duplicate records in the Customer table.
5. Display the customer id, region name, transaction type and transaction amount for the minimum transaction amount in deposit.
6. Create a stored procedure to display details of customers in the Transaction table where the transaction date is greater than Jun 2020.
7. Create a stored procedure to insert a record in the Continent table.
8. Create a stored procedure to display the details of transactions that happened on a specific day.
9. Create a user defined function to add 10% of the transaction amount in a table.
10. Create a user defined function to find the total transaction amount for a given transaction type.
11. Create a table value function which comprises the columns customer_id, region_id ,txn_date , txn_type , txn_amount which will retrieve data from the above table.
12. Create a TRY...CATCH block to print a region id and region name in a single column.
13. Create a TRY...CATCH block to insert a value in the Continent table.
14. Create a trigger to prevent deleting a table in a database.
15. Create a trigger to audit the data in a table.
16. Create a trigger to prevent login of the same user id in multiple pages.
17. Display top n customers on the basis of transaction type.

## Tools Used
- Excel: For Data cleaning and optimization
- MS SQL: For Data Analysis

## Data Analysis: 
Find duplicate records in the Customer table.
```sql 
SELECT c1.customer_id, c1.region_id, c1.start_date, c1.end_date
FROM Customers c1
INNER JOIN Customers c2
ON c1.customer_id = c2.customer_id AND c1.region_id = c2.region_id AND c1.start_date = c2.start_date
AND c1.end_date = c2.end_date AND c1.customer_id <> c2.customer_id

-- to avoid comparing the same record
GROUP BY c1.customer_id, c1.region_id, c1.start_date, c1.end_date
HAVING COUNT(*) > 1;
```
Create a user defined function to add 10% of the transaction amount in a table.
```sql 
CREATE FUNCTION AddTenPercent (@txn_amount DECIMAL(10,2))
RETURNS DECIMAL(10,2)
AS
BEGIN
DECLARE @result DECIMAL(10,2)
SET @result = @txn_amount + (@txn_amount * 0.1)
RETURN @result
END

--call the function
SELECT customer_id, txn_date, txn_type, txn_amount, dbo.AddTenPercent(txn_amount) AS txn_amount_with_10_percent
FROM Trans
```
All the remaing queries is available in the "SQL Case Study 3" pdf format.

## Results 
Here are some key learnings that can be derived from the queries, stored procedures, and functions developed for this case study:

- Understanding Customer Behavior: By analyzing transaction data, one can gain insights into customer behavior, preferences, and trends. This understanding is crucial for providing tailored services and enhancing customer satisfaction.
- Data Management Best Practices: Developing queries to identify duplicate records and managing data effectively ensures database integrity and accuracy. It highlights the importance of data cleansing and maintenance practices.
- Financial Analysis: Calculating total transaction amounts and analyzing transaction patterns helps in financial analysis and decision-making. It enables the bank to optimize its services and offerings based on transaction types and amounts.
- Efficiency through Stored Procedures: Creating stored procedures streamlines repetitive tasks and enhances operational efficiency. Procedures like retrieving transactions after a specific date or inserting records simplify database management.
- Enhanced Functionality with User-Defined Functions: User-defined functions add flexibility and customization to SQL queries. Functions like calculating percentage increases or aggregating transaction amounts provide additional functionality for analysis.
- Geographical Insights: Understanding the distribution of customers across different regions helps in geographic targeting and market segmentation. It enables the bank to tailor its services to meet the specific needs of customers in different regions.
- Compliance and Security Measures: Implementing triggers to prevent unauthorized actions, such as deleting tables or logging in with the same user ID on multiple pages, ensures compliance with security protocols and safeguards sensitive data.


Thank you 
