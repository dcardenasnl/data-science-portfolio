## Week 4 - Code Test

All of the questions in this quiz refer to the open source Chinook Database.
Please familiarize yourself with the ER diagram in order to familiarize
yourself with the table and column names in order to write accurate queries
and get the appropriate an

<img src="ChinookDatabaseSchema.png"
     alt="Markdown Monster icon"
     style="float: left; margin-right: 10px;" />

(Answers were removed)

##### 1. Pull a list of customer ids with the customer’s full name, and address, along with combining their city and country together. Be sure to make a space in between these two and make it UPPER CA

 * What is the city and country result for CustomerID 16?

```sql
SELECT CustomerId, FirstName || ' ' || Lastname as Fullname, Address, UPPER(City || ' ' || Country) as 'City and Country'
FROM Customers
```

##### 2. Create a new employee user id by combining the first 4 letter of the employee’s first name with the first 2 letters of the employee’s last name. Make the new field lower case and pull each individual step to show your work

 * What is the final result for Robert King?
ANS: robek
```sql
SELECT LOWER(substr(FirstName, 1, 4) || substr(Lastname, 1, 2)) as NameID
FROM Employees
```

##### 3. Show a list of employees who have worked for the company for 15 or more years using the current date function. Sort by lastname ascending.

 * What is the lastname of the last person on the list returned?
```sql
SELECT FirstName, LastName, strftime('%Y', 'now') - strftime('%Y', HireDate) as WorkTime
FROM Employees
WHERE WorkTime>=15
```

##### 4. Profiling the Customers table, answer the following question.

Are there any columns with null values? Indicate any below.
Select all that apply.

ANS: PostalCode, Fax, Phone, Company
```sql
SELECT PostalCode, Fax, Phone, Address, FirstName, Company
FROM Customers
WHERE Company is NULL
```

##### 5. Find the cities with the most customers and rank in descending order.

Which of the following cities indicate having 2 customers?

```sql
SELECT COUNT(*) as NumCustomers, City
FROM Customers
GROUP BY City
ORDER BY NumCustomers DESC
```

##### 6. Create a new customer invoice id by combining a customer’s invoice id with their first and last name while ordering your query in the following order: firstname, lastname, and invoiceID

Select all of the correct "AstridGruber" entries that are returned in your results below. Select all that apply

```sql
SELECT c.FirstName, c.Lastname, c.FirstName || c.Lastname || i.InvoiceId as invoiceID2
FROM Invoices i LEFT JOIN Customers c ON i.CustomerId == c.CustomerId
WHERE invoiceID2 LIKE 'AstridGruber%'
```
