# Indexes in MySQL

```
CREATE INDEX email_index ON Users(email);

SELECT * 
FROM Users 
WHERE email LIKE 'h%' 
USE INDEX (email_index);
```
- `CREATE INDEX`: Creates an index on the email column.
- `SELECT`: Queries the Users table for all rows where the email starts with 'h'.
- `USE INDEX`: Informs MySQL to prefer using the email_index when executing this query.
