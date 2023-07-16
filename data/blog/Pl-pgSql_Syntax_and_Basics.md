---
title: PgSql Syntax Basics
date: '2021-05-17'
tags: ['postgres', 'pgsql', 'control structures']
draft: false
summary: Pgsql basic control structures & Crosstab Examples
images: []
layout: PostLayout
canonicalUrl:
---

# Pl/pgSql Syntax and Basics

## **Function Syntax**

```
CREATE OR REPLACE FUNCTION sum(p1 type, p2 type) RETURNS return_type AS
$$
	BEGIN
		--statements
	END;
$$

LANGUAGE plpgsql
```

```
DO
$$
	DECLARE
			CNT INTEGER;
	BEGIN
			SELECT COUNT(*) INTO CNT FROM ACTOR A;
			RAISE NOTICE 'COUNT IS %',CNT;
	END;
$$
```

**Block Structure in pgSql**

```
[ <<label>> ]
[ DECLARE
	declarations]
	BEGIN
		statements;
	END; [ label ];
```

Example:

```
DO
$$
	DECLARE
		mynum                 integer :=1;
		first_name           varchar(100) := 'Sai';
		emptyvar             integer;
	BEGIN
		RAISE NOTICE 'Variables are  % % %',
		mynum,
		first_name,
		emptyvar;
	END;
$$

```

**Accessing a table column Data Type**

```
DO
$$
    DECLARE
        first_name employees.first_name%TYPE;
        prod_name  products.product_name%TYPE
    BEGIN
        RAISE NOTICE 'My name is %',
        first_name;
    END;
$$
```

**Storing result from expressions in a variable**

```
D0
$$
    DECLARE
        row_product record;
    BEGIN
        SELECT
        *
        FROM products
        INTO row_product
        WHERE
            product_id = 1
        LIMIT 1;

        RAISE NOTICE 'Your product is %', row_product.product.id;
    END
$$
```

**Function input & output using IN and OUT**

```
create or replace function fn_sum_2(in x integer, in y integer, out z integer, out w integer) as
$$
	begin
		z = x + y;
		w = x * y;
	end;
$$
language PLPGSQL;
```

**Return results of a query**

```
CREATE OR REPLACE FUNCTION fn_get_latest_payments() RETURNS SETOF payment  AS
$$
	BEGIN
		RETURN QUERY SELECT * FROM payment p ORDER BY p.payment_date DESC;
	END;
$$
LANGUAGE PLPGSQL;
```

**Return a column of table as function output**

```
CREATE OR REPLACE FUNCTION fn_get_latest_payment_id() RETURNS  TABLE("payment_id" integer)  AS
$$
	BEGIN
		RETURN QUERY SELECT p.payment_id  FROM payment p ORDER BY p.payment_date DESC;
	END;
$$
LANGUAGE PLPGSQL;
```

---

##

## **Control Flow**

**IF STATEMENT**

- **Even Odd function**

```
CREATE OR REPLACE FUNCTION fn_is_number_odd(IN num integer) RETURNS text  AS
$$
	DECLARE
		temp integer = num;
	BEGIN
		IF num%2 = 0 THEN
			RETURN 'EVEN';
		ELSE
			RETURN 'ODD';
		END IF;
	END;
$$ LANGUAGE PLPGSQL;
```

- Max of two number

```
CREATE OR REPLACE FUNCTION fn_max(IN a integer, IN b integer) RETURNS integer AS
$$
	BEGIN
		IF a > b THEN
			RETURN a;
		ELSIF a < b THEN
			RETURN b;
		ELSE
			RETURN a;
		END IF;
	END;
$$ LANGUAGE PLPGSQL;
```

**LOOP  STATEMENTS**

**Loop**

Syntax

```
LOOP
	stmt
	EXIT;
END LOOP

LOOP
	stmt
	EXIT WHEN CONDITION con;
END LOOP;

LOOP
	stmt
	IF CONDITION THEN
		EXIT;
	END IF;
END LOOP;
```

- Print first 10 numbers using loop

```
DO
$$
	DECLARE
		counter integer := 1;
	BEGIN
		LOOP
		counter := counter + 1;
		RAISE NOTICE '%',counter;
		IF counter > 10 THEN
			EXIT;
		END IF;
		END LOOP;
	END;
$$
```

#

**For Loop**

Syntax

```
FOR [counter_name] IN [reverse] [START value] .. [END Value] [BY Stepping]
LOOP
	[stmts];
END LOOP;
```

- Print first 10 numbers

```
DO
$$
	BEGIN
		FOR counter IN 1..10
		LOOP
			RAISE NOTICE '%',counter;
		END LOOP;
	END;

$$ LANGUAGE plpgsql
```

- Print Even numbers from 1 to 10

```

DO
$$
	BEGIN
		FOR counter IN 1..10
		LOOP
			IF counter%2 = 0 THEN
					RAISE NOTICE '%',counter;
			END IF;
		END LOOP;
	END;

$$ LANGUAGE plpgsql
```

- Stepping and Reverse in For Loops

```

DO
$$
	BEGIN
		FOR counter IN reverse 10..1 BY 2
		LOOP
			RAISE NOTICE '%',counter;
		END LOOP;
	END;

$$ LANGUAGE plpgsql
```

- Iterate through records in sql statements using FOR LOOP

```
DO
$$
	DECLARE
		rec record;
	BEGIN
		FOR rec IN SELECT actor_id, last_name  FROM actor a
		LOOP               
                    CONTINUE WHEN rec.actor_id % 3 = 0;
		    RAISE NOTICE '%, %', rec.actor_id , rec.last_name ;
		END LOOP;
	END;
$$
```

**For Each Loop**

```
DO
$$
	DECLARE
		rec int[] := ARRAY[20,21,23,50];
		var int;
	BEGIN
		FOREACH var IN ARRAY rec
		LOOP
			RAISE NOTICE '%',var;
		END LOOP;
	END;
$$ LANGUAGE plpgsql;
```

**While loop**

- A function which returns sum of first n numbers, where n is input

```
CREATE OR REPLACE FUNCTION fn_get_sum_till_n(IN n integer) RETURNS integer AS
$$
	DECLARE
		counter integer := 1;
		sum integer := 0;
	BEGIN
		WHILE n > 0
		LOOP
			sum := sum + n;
			n := n - 1;
		END LOOP ;
	RETURN sum;
	END;
$$ LANGUAGE plpgsql
```

- Create a table and insert records into table

```
CREATE OR REPLACE FUNCTION fn_create_table_and_insert(IN n integer) RETURNS boolean AS
$$
	DECLARE
		counter integer := 1;
	BEGIN
		EXECUTE format('create table if not exists temp_table (id int)');
		WHILE counter  <= n
		LOOP
			INSERT INTO temp_table(id) VALUES (counter);
		counter := counter  + 1;
		END LOOP;
		RETURN TRUE;
	END;
$$ LANGUAGE plpgsql
```

**Using RETURN NEXT to return query results**

```
CREATE OR REPLACE FUNCTION fn_get_film_rent_over_limit(IN price integer) RETURNS SETOF film AS
$$
	DECLARE
		rec record;
	BEGIN
		FOR rec IN SELECT * FROM film f WHERE f.rental_rate >= price
		LOOP
			RETURN NEXT rec;
		END LOOP ;
	RETURN;
	END;
$$ LANGUAGE plpgsql;

SELECT fn_get_film_rent_over_limit (4)
```

---

## **Crosstab Reports**

**Install cross tab extension**

```
CREATE EXTENSION IF NOT EXISTS tablefunc;

verify installation

SELECT * FROM  pg_catalog.pg_extension
```

**Syntax**

```
SELECT * FROM crosstab
(
	select_stmt
) AS alias_name
(
	col1 TYPE,
	col2 TYPE,
	...
)
```

The SELECT must RETURN 3 COLUMNS \(x\-axis, y\-axis, values\)

## **Write a sql query to get top n records from each category**

```
select
	*
from
	(
	select
		u.organization,
		u.auth_user_id,
		row_number() over (partition  by <CATEGORY>
	order by
		u.auth_user_id desc) as user_rank
	from
		users u
) ranks
where
	user_rank <= <n>
order by
	organization desc
```

**Miscellaneous**

## Creating Sequences & Adding auto\-increment to column

```
create sequence <table_name>_id_seq;

alter table instyn_videos
    alter column <primary_key_column_name> set default nextval('public.<table_name>_id_seq'::regclass);

alter sequence <table_name>_id_seq owned by <table_name>.id;
```
