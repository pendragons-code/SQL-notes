<details>

<summary>Delimiters are not in the syllabus, but are used with if statements in some cases, expand this to find out more!</summary>

In MySQL, the DELIMITER command is used to change the default delimiter (semicolon `;`) that signals the end of a SQL statement. This is particularly important when creating stored procedures, functions, or triggers that contain multiple SQL statements.

### Why DELIMITER is Needed

By default, MySQL uses a semicolon (`;`) to determine the end of a SQL statement. However, when creating complex database objects like stored procedures, you need to create multiple statements within a single block. Without changing the delimiter, MySQL would interpret each semicolon as the end of the statement, breaking your code.

### Example Without DELIMITER

```sql
CREATE PROCEDURE simple_procedure()
BEGIN
    SELECT 'First statement';
    SELECT 'Second statement';
END;  // This would cause an error
```

### Example With DELIMITER

```sql
DELIMITER //

CREATE PROCEDURE simple_procedure()
BEGIN
    SELECT 'First statement';
    SELECT 'Second statement';
END //

DELIMITER ;
```

### Key Points About DELIMITER:

1. **Temporary Change**: It temporarily changes the statement terminator
2. **Common Alternatives**: While `//` is most common, you can use other characters like `$$`
3. **Reset Needed**: Always reset to `;` after creating your procedure
4. **Scope**: It affects only the current session

### Detailed Breakdown

```sql
-- Change delimiter to //
DELIMITER //

-- Create procedure with multiple statements
CREATE PROCEDURE example_procedure()
BEGIN
    -- Multiple SQL statements can now use ;
    INSERT INTO logs (message) VALUES ('Procedure started');
    UPDATE users SET status = 'active' WHERE id = 1;
    SELECT 'Procedure completed' AS result;
END // 

-- Reset delimiter back to ;
DELIMITER ;
```

### Why Use Different Delimiters?

- Allows multiple SQL statements within a single block
- Prevents MySQL from interpreting internal semicolons as statement terminators
- Essential for creating:
  - Stored Procedures
  - Triggers
  - Functions
  - Complex database objects

### Common Practices:

- Most developers use `//` or `$$`
- Always remember to reset to `;`
- Use it only when creating complex database objects

Would you like me to provide more context or explain any part of this in more detail?
</details>


# MySQL IF and IF EXISTS Guide

## 1. Basic IF Statement in MySQL

In MySQL, conditional logic can be implemented using several methods:

### 1.1 IF Statement in Stored Procedures
```sql
DELIMITER //

CREATE PROCEDURE CheckAge(IN userAge INT)
BEGIN
    IF userAge >= 18 THEN
        SELECT 'You are an adult' AS age_status;
    ELSE
        SELECT 'You are a minor' AS age_status;
    END IF;
END //

DELIMITER ;
```

### 1.2 IF Function for Simple Conditions
```sql
-- Syntax: IF(condition, value_if_true, value_if_false)
SELECT 
    name, 
    salary, 
    IF(salary > 50000, 'High Salary', 'Low Salary') AS salary_category 
FROM employees;
```

## 2. IF EXISTS in MySQL

### 2.1 Checking Table Existence
```sql
-- Method 1: Using Information Schema
IF EXISTS (
    SELECT 1 
    FROM information_schema.tables 
    WHERE table_schema = 'your_database_name' 
    AND table_name = 'employees'
) THEN
    DROP TABLE employees;
END IF;

-- Method 2: Using SHOW TABLES
IF EXISTS (SHOW TABLES LIKE 'employees') THEN
    DROP TABLE employees;
END IF;
```

### 2.2 Conditional Insert or Update
```sql
DELIMITER //

CREATE PROCEDURE UpsertCustomer(
    IN p_customer_id INT, 
    IN p_name VARCHAR(100)
)
BEGIN
    IF EXISTS (SELECT 1 FROM customers WHERE customer_id = p_customer_id) THEN
        -- Update existing customer
        UPDATE customers 
        SET name = p_name 
        WHERE customer_id = p_customer_id;
    ELSE
        -- Insert new customer
        INSERT INTO customers (customer_id, name) 
        VALUES (p_customer_id, p_name);
    END IF;
END //

DELIMITER ;
```

## 3. Advanced Conditional Handling

### 3.1 Multiple Conditions
```sql
DELIMITER //

CREATE PROCEDURE ClassifyEmployee(IN salary DECIMAL)
BEGIN
    IF salary < 30000 THEN
        SELECT 'Entry Level' AS employee_level;
    ELSEIF salary BETWEEN 30000 AND 50000 THEN
        SELECT 'Mid Level' AS employee_level;
    ELSE
        SELECT 'Senior Level' AS employee_level;
    END IF;
END //

DELIMITER ;
```

## 4. CASE Statement Alternative
```sql
SELECT 
    name, 
    CASE 
        WHEN age < 18 THEN 'Minor'
        WHEN age BETWEEN 18 AND 65 THEN 'Adult'
        ELSE 'Senior'
    END AS age_category
FROM users;
```

## 5. Best Practices

- Always use `DELIMITER` when creating stored procedures
- Be careful with nested conditional statements
- Use appropriate indexes for performance
- Handle NULL values explicitly

## 6. Common Pitfalls

- Forgetting to reset `DELIMITER`
- Not handling NULL conditions
- Overcomplicating conditional logic
- Performance issues with complex nested conditions

## 7. Performance Considerations

- Prefer `CASE` statements for simple lookups
- Use indexed columns in conditional checks
- Avoid multiple nested `IF` statements
- Consider using prepared statements for repeated queries
