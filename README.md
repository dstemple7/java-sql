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

|    Pet Types        | PET OWNER by ID            | PET OWNER by ID            |            |            |            |            |            |            |
|------------|------------|------------|------------|------------|------------|------------|------------|------------|
|    Dog        |    0        |      3      |            |            |            |            |            |            |
|    Horse        |   2         |            |            |            |            |            |            |            |
|    Cat        |      0      |       3     |            |            |            |            |            |            |
|    Turtle        |    0        |            |            |            |            |            |            |            |
|    Fish        |       3     |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |
|            |            |            |            |            |            |            |            |            |

Table Name: PETS by PET TYPE

|    ID        |   PET TYPE         |            |            |            |            |            |            |            |
|------------|------------|------------|------------|------------|------------|------------|------------|------------|
|    0        |     Dog       |            |            |            |            |            |            |            |
|     1       |     Cat       |            |            |            |            |            |            |            |
|      2      |     Turtle       |            |            |            |            |            |            |            |
|       3     |     Horse       |            |            |            |            |            |            |            |
|        4    |     Dog       |            |            |            |            |            |            |            |
|         5   |     Cat       |            |            |            |            |            |            |            |
|          6  |     Fish       |            |            |            |            |            |            |            |

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
DELETE
FROM customers
WHERE customer_id NOT IN (SELECT customer_id FROM orders)
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
--
-- PostgreSQL database dump
--

-- Dumped from database version 12.3
-- Dumped by pg_dump version 12.3

-- Started on 2020-08-05 17:52:06

SET statement_timeout = 0;
SET lock_timeout = 0;
SET idle_in_transaction_session_timeout = 0;
SET client_encoding = 'UTF8';
SET standard_conforming_strings = on;
SELECT pg_catalog.set_config('search_path', '', false);
SET check_function_bodies = false;
SET xmloption = content;
SET client_min_messages = warning;
SET row_security = off;

SET default_tablespace = '';

SET default_table_access_method = heap;

--
-- TOC entry 202 (class 1259 OID 16728)
-- Name: accounts; Type: TABLE; Schema: public; Owner: postgres
--

CREATE TABLE public.accounts (
    id integer NOT NULL,
    name character(1) NOT NULL,
    budget numeric NOT NULL
);


ALTER TABLE public.accounts OWNER TO postgres;

--
-- TOC entry 203 (class 1259 OID 16731)
-- Name: accounts_id_seq; Type: SEQUENCE; Schema: public; Owner: postgres
--

CREATE SEQUENCE public.accounts_id_seq
    AS smallint
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE public.accounts_id_seq OWNER TO postgres;

--
-- TOC entry 2826 (class 0 OID 0)
-- Dependencies: 203
-- Name: accounts_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: postgres
--

ALTER SEQUENCE public.accounts_id_seq OWNED BY public.accounts.id;


--
-- TOC entry 2688 (class 2604 OID 16739)
-- Name: accounts id; Type: DEFAULT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.accounts ALTER COLUMN id SET DEFAULT nextval('public.accounts_id_seq'::regclass);


--
-- TOC entry 2819 (class 0 OID 16728)
-- Dependencies: 202
-- Data for Name: accounts; Type: TABLE DATA; Schema: public; Owner: postgres
--

COPY public.accounts (id, name, budget) FROM stdin;
\.


--
-- TOC entry 2827 (class 0 OID 0)
-- Dependencies: 203
-- Name: accounts_id_seq; Type: SEQUENCE SET; Schema: public; Owner: postgres
--

SELECT pg_catalog.setval('public.accounts_id_seq', 1, false);


--
-- TOC entry 2690 (class 2606 OID 16751)
-- Name: accounts id; Type: CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.accounts
    ADD CONSTRAINT id PRIMARY KEY (id);


--
-- TOC entry 2692 (class 2606 OID 16753)
-- Name: accounts name; Type: CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.accounts
    ADD CONSTRAINT name UNIQUE (name);


-- Completed on 2020-08-05 17:52:06

--
-- PostgreSQL database dump complete
--
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
