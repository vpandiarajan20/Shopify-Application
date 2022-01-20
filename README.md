# Shopify Application
Data Science

Part 1:
Data Analysis:
a. Our analysis shows that the average order values are mostly reasonable, but there is at least one outlier in the data. There is an order for over 700,000 which is responsible for the average order value being so high.

b. I would report the median order value. This statistic is far more helpful in gaining a sense of where the majority of the data lies. If allowed, I would also report the top of the first quartile and the top of the third quartile, as they would give you a very good sense of the range of the data.

c. The median order value is 284 and the the top of the first quartile is 163 and the top of the third quartile is 390.

Part 2:
SQL Queries:

SELECT COUNT(ORDERID) FROM [Orders]
WHERE ShipperID=1

SELECT LastName FROM 
	(SELECT Orders.EmployeeID, Employees.LastName, Orders.OrderID FROM Orders
	INNER JOIN Employees ON Orders.EmployeeID=Employees.EmployeeID)
GROUP BY LastName
ORDER BY COUNT(ORDERID) DESC
LIMIT 1;

SELECT ProductName FROM
(SELECT OrderDetails.ProductID, OrderDetails.Quantity, Products.ProductName FROM Customers AS newTable
  INNER JOIN Orders ON Orders.CustomerID=newTable.CustomerID
  LEFT JOIN OrderDetails ON Orders.OrderID=OrderDetails.OrderID
  LEFT JOIN Products ON Products.ProductID=OrderDetails.ProductID
  WHERE newTable.Country='Germany')
GROUP BY ProductID
ORDER BY SUM(Quantity) DESC
LIMIT 1;
