# Basic parts of SQL code

```
CREATE DATABASE Users;
```

* The above is a **Statement** :
  + It is made with 1 or more lines of code.
  + It also ends with a semi-colon.

* In the above statement, there are **Keywords** .
  + This tells SQL that you are performing certain instructions or actions.
  + In this example, the keywords are `CREATE` and `DATABASE`.

* In this statement there is also an **Identifier** 
  + The Identifier tells SQL what the identity of a specific "item" is.
# Data Types and Constraints

```
CREATE TABLE Users(
	id INT PRIMARY KEY AUTO_INCREMENT,
	email VARCHAR(255) NOT NULL UNIQUE,
	bio TEXT,
	country VARCHAR(2)
);
```

In the statement above, inside the table `Users` , there are **Identifiers**, **Constraints** and **Data Types** 

	

* The Data Types used here are `INT`,  `VARCHAR` and `TEXT`.
  + `INT` means Integer.
  + `VARCHAR` is a variable character field, it is for the most part a string with a length limit.
  + `TEXT` represents a string of unspecified length.

* The **Identifier** here are `id`,  `bio`,  `email` and `country`

* The **Constraints** here are `PRIMARY KEY`,  `AUTO_INCREMENT`,  `NOT NULL` and `UNIQUE`. (technically the numers in the varchars are also constraints).
  + `PRIMARY KEY` is the key that is a columnin a table that is distinctive for each record
  + `AUTO INCREMENT` is a constraint that tells the db to automatically increase the value for every newly added entry
  + `NOT NULL` makes it so a field in a table cannot be empty
  + `UNIQUE` ensures that there are no duplicates


# Schema
A database schema is a blueprint that defines the **structure**, **organization**, and **relationships** of a database.