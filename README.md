# 🧠💾 The Semi-Colons ;

> "Because life without semicolons is just a series of syntax errors." 😄

---

## 👥 Group Members
- **Moise Ishimwe**
- **[Your Teammate’s Name]**

---

## 📌 Project Title
**Mastering SQL Window Functions Like Pros** 🚀

---

## 🎯 Objective
The goal of this project is to demonstrate the power of **SQL Window Functions** through a series of real-world analytical queries. We use a mock employee dataset to:
- Compare records with `LAG()` and `LEAD()`
- Rank data using `RANK()` and `DENSE_RANK()`
- Extract top and earliest records using `RANK()` and `ROW_NUMBER()`
- Use `MAX()` with `PARTITION BY` for aggregation
- Provide real-life applications
- Document and visualize our queries with results

---

## 🗂️ Repository Structure
```
The-Semi-Colons/
├── create_table_and_insert_data.sql
├── lag_lead_comparison.sql
├── ranking_within_category.sql
├── top_3_per_category.sql
├── earliest_records.sql
├── windowed_aggregation.sql
└── README.md
```

---

## 📊 Dataset Overview
Our project is based on a fictional `employees` table with the following structure:

| Column      | Description             |
|-------------|-------------------------|
| emp_id      | Unique Employee ID      |
| emp_name    | Employee's Name         |
| department  | Department Name         |
| salary      | Monthly Salary          |
| hire_date   | Date Hired              |

---

## 🏗️ Table Creation & Sample Data Insertion
**File**: `create_table_and_insert_data.sql`

```sql
CREATE TABLE employees (
  emp_id INT PRIMARY KEY,
  emp_name VARCHAR(100),
  department VARCHAR(50),
  salary INT,
  hire_date DATE
);

INSERT INTO employees (emp_id, emp_name, department, salary, hire_date) VALUES
(1, 'Alice', 'HR', 5000, '2020-01-15'),
(2, 'Bob', 'HR', 5500, '2019-03-10'),
(3, 'Charlie', 'IT', 7000, '2021-06-01'),
(4, 'Diana', 'IT', 7000, '2021-07-20'),
(5, 'Eve', 'IT', 7200, '2018-11-23'),
(6, 'Frank', 'Marketing', 4000, '2020-05-14'),
(7, 'Grace', 'Marketing', 4000, '2021-09-01'),
(8, 'Heidi', 'Marketing', 4500, '2019-12-11'),
(9, 'Ivan', 'HR', 5200, '2022-01-05'),
(10, 'Judy', 'IT', 7100, '2023-04-18');
```

### 📝 Explanation
We created a simple but realistic dataset of employees, distributed across different departments with varied salaries and hire dates. This setup helps in performing accurate window function analysis.

---

## 1️⃣ Compare with Previous and Next Records – `LAG()` & `LEAD()`
**File**: `lag_lead_comparison.sql`

```sql
SELECT
  emp_id, emp_name, department, salary,
  LAG(salary) OVER (PARTITION BY department ORDER BY salary) AS prev_salary,
  LEAD(salary) OVER (PARTITION BY department ORDER BY salary) AS next_salary,
  CASE 
    WHEN salary > LAG(salary) OVER (PARTITION BY department ORDER BY salary) THEN 'HIGHER'
    WHEN salary < LAG(salary) OVER (PARTITION BY department ORDER BY salary) THEN 'LOWER'
    ELSE 'EQUAL'
  END AS comparison_to_prev
FROM employees;
```

### 📝 Explanation
Compares current salary to the previous and next salary within each department.

### 📸 Screenshot of Output
`Insert your screenshot here`

### ✅ Real-life Use
Useful for HR departments to track salary progression.

---

## 2️⃣ Rank Within Each Department – `RANK()` & `DENSE_RANK()`
**File**: `ranking_within_category.sql`

```sql
SELECT 
  emp_id, emp_name, department, salary,
  RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank_standard,
  DENSE_RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank_dense
FROM employees;
```

### 📝 Explanation
- `RANK()` skips ranks for ties
- `DENSE_RANK()` doesn’t skip any rank numbers

### 📸 Screenshot of Output
`Insert your screenshot here`

### ✅ Real-life Use
Determine fair ranking among employees or students.

---

## 3️⃣ Top 3 Salaries per Department
**File**: `top_3_per_category.sql`

```sql
WITH ranked_emps AS (
  SELECT *,
    RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank_position
  FROM employees
)
SELECT * FROM ranked_emps WHERE rank_position <= 3;
```

### 📝 Explanation
Uses a CTE to rank and filter top 3 earners per department.

### 📸 Screenshot of Output
`Insert your screenshot here`

### ✅ Real-life Use
Performance reviews and rewards allocation.

---

## 4️⃣ First 2 Employees per Department – `ROW_NUMBER()`
**File**: `earliest_records.sql`

```sql
WITH first_emps AS (
  SELECT *,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY hire_date) AS row_num
  FROM employees
)
SELECT * FROM first_emps WHERE row_num <= 2;
```

### 📝 Explanation
Finds the first two employees to be hired in each department.

### 📸 Screenshot of Output
`Insert your screenshot here`

### ✅ Real-life Use
Identify veteran staff or earliest customers.

---

## 5️⃣ Aggregation with Window Functions – `MAX()` OVER
**File**: `windowed_aggregation.sql`

```sql
SELECT 
  emp_id, emp_name, department, salary,
  MAX(salary) OVER (PARTITION BY department) AS dept_max_salary,
  MAX(salary) OVER () AS overall_max_salary
FROM employees;
```

### 📝 Explanation
Displays maximum salaries per department and across the whole company.

### 📸 Screenshot of Output
`Insert your screenshot here`

### ✅ Real-life Use
Benchmarking salary standards across teams.

---

## 📌 Real-Life Applications Summary
| Function | Application Examples |
|---------|----------------------|
| `LAG`, `LEAD` | Salary trends, sales growth |
| `RANK`, `DENSE_RANK` | Student performance, leaderboards |
| `ROW_NUMBER` | Hiring order, customer acquisition |
| `MAX() OVER()` | Department-wise and company-wide performance |

---

## 🧰 Tech Stack
- 🐘 PostgreSQL
- 📂 Git & GitHub
- 📜 Markdown for documentation

---

## 👨‍🏫 Instructor Access
- ✅ Collaborator Added: `ericmaniraguha`

---

## 🗓️ Submission Details
- 📅 **Deadline**: April 17, 2025 at 11:59 PM
- 📎 **Submission**: GitHub Repository Link

---

## 🙏 Special Thanks
To our instructor for this exciting challenge and to our team for the collaboration! 🚀

---

## 🎉 Fun Fact
> Why did the SQL developer break up with the semicolon? 
> Because it was too **terminating**! 😂








