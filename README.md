CREATE TABLE Employees(
	EmpID INT PRIMARY KEY NOT NULL,
  	Name VARCHAR(50),
  	DeptID INTEGER , 
  	Salary INTEGER NOT NULL,
  	City VARCHAR(100)
);

CREATE TABLE Departments(
	DeptID INT PRIMARY KEY AUTO_INCREMENT,
  	DeptName VARCHAR(100)
);

INSERT INTO Employees VALUES(101 , 'Alice',	1,60000,'New York'),(102,'Bob',2,45000,'Chicago'),(103 ,'Charlie',1, 75000 ,'New York'),(104 ,'David',3,50000,'Boston'),(105,'Eve',2,55000,'Chicago');

INSERT INTO Departments(DeptName) VALUES('Engineering'),('MarKeting'),('Sales')


-- QUery
SELECT * FROM Employees;
SELECT * FROM Departments;

SELECT Name 
FROM Employees
INNER JOIN Departments AS DEP
WHERE DEP.DeptID = Employees.DeptID;

SELECT Emp.Name
FROM Employees AS Emp
INNER JOIN Departments AS DEP ON Emp.DeptID = DEP.DeptID
WHERE DEP.DeptName = 'MarKeting';

SELECT Name, Salary 
FROM Employees 
WHERE Salary > 52000
ORDER BY Salary DESC;

SELECT DEP.DeptName, SUM(EMP.Salary)
FROM Departments AS DEP
INNER JOIN Employees AS EMP ON DEP.DeptID = EMP.DeptID 
GROUP BY DEP.DeptName;

SELECT EMP.Name 
FROM Employees AS EMP 
INNER JOIN Departments AS DEP ON EMP.DeptID = DEP.DeptID
WHERE DEP.DeptName = 'Engineering' AND EMP.City = 'New York';

SELECT EMP.Name 
FROM Employees AS EMP 
LEFT JOIN Departments AS DEP ON EMP.DeptID = EMP.DeptID
WHERE EMP.EmpID IS NULL; 
