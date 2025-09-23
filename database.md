## SQL

 Sharding
	Sharding is optimization technique.Which will help Database to scale horizontally

 Particians
	Split the large database into smaller sets to increase performence.we can wuery only that particean so data performence is good
	We can arcaive data by particean is easy
	
   RANGE Partitioning
	CREATE TABLE sales (
	    id INT,
	    sale_date DATE,
	    amount DECIMAL(10,2)
	)
	PARTITION BY RANGE (YEAR(sale_date)) (
	    PARTITION p0 VALUES LESS THAN (2021),
	    PARTITION p1 VALUES LESS THAN (2022),
	    PARTITION p2 VALUES LESS THAN (2023),
	    PARTITION p3 VALUES LESS THAN MAXVALUE
	);
  LIST Partitioning
	CREATE TABLE employees (
	    id INT,
	    name VARCHAR(50),
	    department_id INT
	)
	PARTITION BY LIST (department_id) (
	    PARTITION p1 VALUES IN (1, 2, 3),
	    PARTITION p2 VALUES IN (4, 5),
	    PARTITION p3 VALUES IN (6, 7, 8)	
	);
HASH Partitioning
	CREATE TABLE orders (
	    id INT,
	    customer_id INT
	)
	PARTITION BY HASH(customer_id) PARTITIONS 4;

KEY Partitioning
	CREATE TABLE users (
	    id INT NOT NULL,
	    name VARCHAR(50),
	    PRIMARY KEY(id)
	)
	PARTITION BY KEY(id) PARTITIONS 4;

What is WITH in SQL?

WITH is used to define a CTE (Common Table Expression).

It’s like creating a temporary, named result set that you can reuse in your query.

Improves readability, avoids repeating subqueries, and is useful for recursive queries.

🔹 Basic Syntax		

WITH cte_name AS (
    SELECT ...
)
SELECT * FROM cte_name;

Recursive with
WITH RECURSIVE manager_hierarchy AS (
    SELECT id, name, manager_id
    FROM employees
    WHERE manager_id IS NULL   -- top manager (CEO)

    UNION ALL

    SELECT e.id, e.name, e.manager_id
    FROM employees e
    INNER JOIN manager_hierarchy mh ON e.manager_id = mh.id
)
SELECT * FROM manager_hierarchy;

Window Functions
	function_name(expression) 
OVER (
    PARTITION BY column   -- optional (like GROUP BY)
    ORDER BY column       -- optional (defines row order)
    ROWS/RANGE clause     -- optional (sliding window)
)

ROW_NUMBER()
	SELECT name, department, salary,
	       ROW_NUMBER() OVER(PARTITION BY department ORDER BY salary DESC) AS rank_in_dept
	FROM employees;
RANK() and DENSE_RANK()

	RANK() → gives gaps if ties exist.

	DENSE_RANK() → no gaps for ties.

SELECT name, salary,
       RANK() OVER(ORDER BY salary DESC) AS rank_with_gaps,
       DENSE_RANK() OVER(ORDER BY salary DESC) AS dense_rank_no_gaps
FROM employees;

NTILE(n)

Divides rows into n groups (buckets).
SELECT name, salary,
       NTILE(4) OVER(ORDER BY salary DESC) AS quartile
FROM employees;

ggregate Functions as Window Functions
	You can use SUM(), AVG(), MIN(), MAX(), COUNT() with a window.
	SELECT name, department, salary,
	       AVG(salary) OVER(PARTITION BY department) AS dept_avg_salary
	FROM employees;

LEAD() and LAG()

	LAG() → get previous row’s value.

	LEAD() → get next row’s value.
	SELECT name, salary,
	       LAG(salary) OVER(ORDER BY hire_date) AS prev_salary,
	       LEAD(salary) OVER(ORDER BY hire_date) AS next_salary
	FROM employees;

Find the top 3 highest-paid employees in each department

SELECT department, name, salary
FROM (
    SELECT department, name, salary,
           ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rnk
    FROM employees
) t
WHERE rnk <= 3;

Options 2
WITH deparment_rank as(
SELECT department, name, salary,
           ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rnk
    FROM employees
)
SELECT department, name, salary FROM deparment_rank where rnl<=3



