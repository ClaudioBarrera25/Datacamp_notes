# Parsing and manipulating text

`CHAR LENGTH`

`SELECT title, CHARLENGTH(title) FROM film;`

returns amount of characters as integer

`LENGTH(title)`

is also an analogous option to CHARLENGTH

## Position

`SELECT email, POSITION('@' IN email) FROM customer;`

`SELECT email, STRPOS(email,'@') FROM customer;`

both are analogous, find the first occurrence.

## Parsing

`SELECT LEFT(description,50)`

`SELECT RIGHT(description,50)`

`SELECT SUBSTRING(description,10,50) FROM film AS f;`

You can use substring to retrieve specific amount of info

`SELECT SUBSTRING(email FROM 0 FOR POSITION('@' in email))`

To return after the @ would be 

`SELECT SUBSTRING(email FROM POSITION('@' in email)+1 FOR CHAR_LENGTH(email))`

`SELECT SUBSTR(description, 10, 50)`

# Truncating and padding string data

`TRIM([leading|trailing|both] [characters] from string)`

`SELECT TRIM('  padded   ');`

Also exist LTRIM and RTRIM.

`SELECT LPAD('padded', 10, '#')`

Retorna '###padded', so the length of the word is 10. default is blank space.


# Introduction to full-text search

LIKE OPERATOR

_ wildcard: Used to match exactly one character

% wildcard: Used to match zero or more characters, is case sensitive


full-text search, is case insensitive

`SELECT title, description FROM film WHERE to_tsvector(title) @@ to_tsquery('elf');`


## Extending postgreSQL

## User defined data types

Enumerated data types

`CREATE TYPE dayofweek AS ENUM('Monday', 'Tuesday','Wednesday');`

Now you can query the data types available

`SELECT typname, typcategory FROM pg_type WHERE typname='dayofweek'`

Also we can use information schema 

`SELECT column_name, data_type, udt_name FROM INFORMATION_SCHEMA.COLUMNS WHERE table_name = 'film';`

With the udt_name, we can find the type name in the pg_type table.


## User defined functions


```
CREATE FUNCTION squared(i integer) RETURNS integer AS $$ 
	BEGIN 
		RETURN i*i;
	END;
$$ LANGUAGE plpgsql;
```
