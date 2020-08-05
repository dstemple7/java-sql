# Java SQL

A student that completes this project shows that they can:

* Query data from a single table
* Query data from multiple tables
* Create a new database using PostgreSQL

## Introduction

Working with SQL

## Instructions

Reimport the Northwind database into PostgreSQL using pgAdmin. This is the same data we used during the guided project.

* [ ] ***pgAdmin data refresh***

* Select the northwind database created during the guided project.

* Tools -> Query Tool
  * Open file northwind.sql (you used this script during the guided project)
  * Execute

* Look under
  * northwind -> Schemas -> public -> tables

* Clear query windows

### Answer the following data queries. Keep track of the SQL you write by pasting it into this document under its appropriate header below in the provided SQL code block. You will be submitting that through the regular fork, change, pull process

* [ ] ***find all customers that live in London. Returns 6 records***
  ```SQL
  SELECT contact_name
  FROM customers
  WHERE city='London'
  ```

* [ ] ***find all customers with postal code 1010. Returns 3 customers***
  ```SQL
  SELECT contact_name
  FROM customers
  WHERE postal_code='1010'
  ```

* [ ] ***find the phone number for the supplier with the id 11. Should be (010) 9984510***
  ```SQL
  SELECT contact_name, phone
  FROM suppliers
  WHERE supplier_id=11
  ```

* [ ] ***list orders descending by the order date. The order with date 1998-05-06 should be at the top***
  ```SQL
  SELECT *
  FROM orders
  ORDER BY order_date DESC
  ```

* [ ] ***find all suppliers who have names longer than 20 characters. Returns 11 records***
  ```SQL
  SELECT company_name
  FROM suppliers
  WHERE LENGTH(company_name) > 20
  ```

* [ ] ***find all customers that include the word 'MARKET' in the contact title. Should return 19 records***
  ```SQL
  SELECT contact_title
  FROM customers
  WHERE UPPER (contact_title) LIKE '%MARKET%'
  ```

* [ ] ***add a customer record for***
  ```SQL
  INSERT 
	  INTO customers(customer_id, company_name, contact_name, address, city, postal_code, country)
	  VALUES('SHIRE', 'The Shire', 'Bilbo Baggins', '1 HObbit-Hole', 'Bag End', '111', 'Middle Earth')
  ```

* [ ] ***update _Bilbo Baggins_ record so that the postal code changes to _"11122"_***
  ```SQL
  UPDATE customers
  SET postal_code = '11122'
  WHERE contact_name = 'Bilbo Baggins'
  ```

* [ ] ***list orders grouped and ordered by customer company name showing the number of orders per customer company name. _Rattlesnake Canyon Grocery_ should have 18 orders***
  ```SQL
  SELECT COUNT(o.customer_id), c.company_name
  FROM customers c JOIN orders o 
  ON o.customer_id = c.customer_id
  GROUP BY c.company_name
  ORDER BY c.company_name DESC
  ```

* [ ] ***list customers by contact name and the number of orders per contact name. Sort the list by the number of orders in descending order. _Jose Pavarotti_ should be at the top with 31 orders followed by _Roland Mendal_ with 30 orders. Last should be _Francisco Chang_ with 1 order***
  ```SQL
  SELECT COUNT(o.customer_id), c.contact_name
  FROM customers c JOIN orders o
  ON o.customer_id = c.customer_id
  GROUP BY c.contact_name
  ORDER BY COUNT DESC
    ```

* [ ] ***list orders grouped by customer's city showing the number of orders per city. Returns 69 Records with _Aachen_ showing 6 orders and _Albuquerque_ showing 18 orders***
  ```SQL
  SELECT COUNT(o.customer_id), c.city
  FROM customers c JOIN orders o
  ON o.customer_id = c.customer_id
  GROUP BY c.city
  ORDER BY c.city
  ```

## Data Normalization

Note: This step does not use PostgreSQL!

* [ ] ***Take the following data and normalize it into a 3NF database***

| Person Name | Pet Name | Pet Type | Pet Name 2 | Pet Type 2 | Pet Name 3 | Pet Type 3 | Fenced Yard | City Dweller |
|-------------|----------|----------|------------|------------|------------|------------|-------------|--------------|
| Jane        | Ellie    | Dog      | Tiger      | Cat        | Toby       | Turtle     | No          | Yes          |
| Bob         | Joe      | Horse    |            |            |            |            | No          | No           |
| Sam         | Ginger   | Dog      | Miss Kitty | Cat        | Bubble     | Fish       | Yes         | No           |

Below are some empty tables to be used to normalize the database

* Not all of the cells will contain data in the final solution
* Feel free to edit these tables as necessary

Table Name: PET OWNER by Person Name

|    Person Name        | ID            | Number of Pets            | Fenced Yard            |City Dweller      |            |            |            |            |
|------------|------------|------------|------------|------------|------------|------------|------------|------------|
|       Jane     |  0          |  3          |      No      |    Yes        |            |            |            |            |
|  Bob          |    1        |    1        |        No    |        No    |            |            |            |            |
|  Sam          |     2       |     3       |        Yes    |        NO    |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |

Table Name: PET TYPES by PET OWNER

|            |            |            |            |            |            |            |            |            |
|------------|------------|------------|------------|------------|------------|------------|------------|------------|
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |

Table Name: PETS by PET TYPE

|            |            |            |            |            |            |            |            |            |
|------------|------------|------------|------------|------------|------------|------------|------------|------------|
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |

Table Name: PETS by PREFERRED PRONOUN [TBD IN FUTURE EXPANSION]

|            |            |            |            |            |            |            |            |            |
|------------|------------|------------|------------|------------|------------|------------|------------|------------|
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |

---

### Stretch Goals

* [ ] ***delete all customers that have no orders. Should delete 2 (or 3 if you haven't deleted the record added) records***

```SQL

```

* [ ] ***Create Database and Table: After creating the database, tables, columns, and constraint, generate the script necessary to recreate the database. This script is what you will submit for review***

* use pgAdmin to create a database, naming it `budget`.
* add an `accounts` table with the following _schema_:

  * `id`, numeric value with no decimal places that should autoincrement.
  * `name`, string, add whatever is necessary to make searching by name faster.
  * `budget` numeric value.

* constraints
  * the `id` should be the primary key for the table.
  * account `name` should be unique.
  * account `budget` is required.

```SQL

```

To see the script

* Right Click on the database name
  * Select Backup...
    * Set a filename
      * To put the file backup.sql in your home directory, you could use `backup.sql`
    * Set format to `Plain`
* The script you want is now in the text file named above.
  * Copy the script from the text file into the SQL code block above!

![Database Script](assets/jx-12-m3-script.gif)
