# CRUD ops in SQL

In this part we will explore CRUD operations in SQL, and how constraints and keywords are put into play to help you achieve the desired results.

| CRUD role | keyword      |
| --------- | ------------ |
| Create    | INSERT       |
| READ      | SELECT       |
| UPDATE    | UPDATE/ALTER |
| DELETE    | DELETE/DROP  |

SIDE: [Wikipedia on CRUD operations (a 7 minute read, word every one).](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)

## CREATE (INSERT)

```
INSERT INTO Users (email, bio, country)

VALUES (
	'hello@world.com',
	'I love tomatoes',
	'US'
);
```

- We do not need to add the `id` field and the respective value. this is because we have already set it to `AUTO INCREMENT`.

If we want to insert multiple rows of data we can do it like so:

```
INSERT INTO Users (email, bio, country)

VALUES
	('hello@world.com', 'I love tomatoes', 'US'),
	('skibidi@toilet.com', 'Skibidi Toilet Is the best!', 'MY');
```

<br>
<br>

## READ (SELECT)

- `SELECT * FROM Users` returns the whole `Users` `table`. Use `*` to specify everything.

<br>

- `Read` the `email` and `id` from the `Users` `table` and `LIMIT` the number of entries to `2`.
  ```
  SELECT email, id FROM Users
  LIMIT 2;
  ```

<br>

- `READ` the `email` and `id`, from `Users`, but `Order` by the `id` it in `Ascending` fashion and `LIMIT` the number of entries to `2`.

  ```
  SELECT email, id FROM Users
  ORDER BY id ASC
  LIMIT 2;
  ```

  - `ASC` for ascending and `DESC` for descending

<br>

- `READ` the `email` and `id`, from `Users`, but `Order` by the `id` it in `Descending` fashion and `LIMIT` the number of entries to `2` and only get the results `Where` the `country` is `US`.

  ```
  SELECT email, id, country FROM Users

  Where country = 'US'

  ORDER BY id DESC
  LIMIT 2;
  ```

  - Adding a chaining condition to make sure all the details above, but `where` the `id` is `more than` `1`.

    ```
    SELECT email, id, country FROM Users

    Where country = 'US'
    AND id > 1

    ORDER BY id DESC
    LIMIT 2;
    ```

  - Adding a bracket can allow you to chain complex conditions, for example:
    ```
    SELECT *
    FROM Employees
    WHERE (Salary > 50000 AND Department = 'HR')
    OR (Salary > 60000 AND Department = 'IT');
    ```

- You can also read by patterns, using the `LIKE` keyword. In this case, where `emails` start with an `h`. (`%` is used like a wildcard character here)

  ```
  SELECT email, id, country FROM Users

  Where country = 'US'
  AND email LIKE 'h%'

  ORDER BY id DESC
  LIMIT 2;
  ```

  - Like is slow for reading, but you can speed the retrieval using database indexes.
  - Indexes, however, use more memory and causes slower writes.
    - Indexes are not in our syllabus, so it will have a dedicated page for it. [Indexes](./index.md)

<br>
<br>

## UPDATE (UPDATE/Alter)
You can actually alter more than just data, you can also alter configs and user details with the `Alter` keyword. so please be careful.

Update `employees` `where` the `name` is `bob`:

```
UPDATE employees
SET salary = 65000
WHERE name = 'Bob';
```


Alter Columns:
- add a column
	```
	ALTER TABLE employees
	ADD email VARCHAR(100);
	```

- change column data type
	```
	ALTER TABLE employees
	MODIFY salary FLOAT;
	```

- rename column from salary to annual_salary and specify data type
	```
	ALTER TABLE employees
	CHANGE salary annual_salary INT;
	```

## DELETE (DELETE/DROP)

`Delete` is used to delete a specific row and `Drop` is used to delete a `Database` or `table`

```
DROP TABLE Users;
DROP DATABASE Users;
```

## DELETING COLUMNS
You need to use both `Delete` and `Alter`. Think of it as, I want to update the `table`, but deleting the `column`.
If you have a table called employees and you want to delete a column named age, the query would look like this:
```
ALTER TABLE employees
DROP COLUMN age;
```