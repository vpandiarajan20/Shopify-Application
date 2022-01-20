# Shopify Application
 Data Science

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