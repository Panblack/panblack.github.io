# Postgresql 9.4

## II. The SQL Language 4. SQL Syntax

### 4.1. Lexical Structure

#### 4.1.1. Identifiers and Key Words
token: A token can be a key word, an identifier, a quoted identifier, a literal (or constant), or a special character symbol. Tokens are normally separated by whitespace (space, tab, newline), but need not be if there is no ambiguity (which is generally only the case if a special character is adjacent to some other token type).

correlation: the name of a table

key words: like SELECT, UPDATE, or VALUES
https://www.postgresql.org/docs/9.4/sql-keywords-appendix.html

identifiers(names): names for tables, collumns and other database objects . case-insensitive , but sensitive if quoted.

#### 4.1.2. Constants

`String:     quoted with ' or $$ or $Tag$ , E'\t\n' , unicode U&'d\0061t\+000061'`

`Bit-string: B'10101' , X'1FF'`

`Numeric:    42 , -3.5 , 4. , .001 , 5e2 , 1.925e-3 , REAL '1.456'`

```
-- Keyword Identifier             Constant
UPDATE     My_Table   SET  A   = 'This is tom''s house.';
UPDATE     "my_table" SET  "a" = E'This is tom\'s house.';

select $$Dianne's horse$$;
select $Tag$Dianne's $$ horse$Tag$;
```

#### 4.1.3. Operators
```
+ - * / < > = ~ ! @ # % ^ & | ` ?
```

#### 4.1.4. Special Characters
-    A dollar sign $ followed by digits is used to represent a positional parameter in the body of a function definition or a prepared statement. In other contexts the dollar sign can be part of an identifier or a dollar-quoted string constant.

-    Parentheses () have their usual meaning to group expressions and enforce precedence. In some cases parentheses are required as part of the fixed syntax of a particular SQL command.

-    Brackets [] are used to select the elements of an array. See Section 8.15 for more information on arrays.

-    Commas , are used in some syntactical constructs to separate the elements of a list.

-    The semicolon ;  terminates an SQL command. It cannot appear anywhere within a command, except within a string constant or quoted identifier.

-    The colon : is used to select "slices" from arrays. (See Section 8.15.) In certain SQL dialects (such as Embedded SQL), the colon is used to prefix variable names.

-    The asterisk * is used in some contexts to denote all the fields of a table row or composite value. It also has a special meaning when used as the argument of an aggregate function, namely that the aggregate does not require any explicit parameter.

-    The period . is used in numeric constants, and to separate schema, table, and column names.


#### 4.1.5. Comments
```
-- This is a comment

/*
   This is a comment
   This is a comment2
*/

```


Table 4-1. Backslash Escape Sequences

Backslash Escape Sequence  | Interpretation
 --- | ---
\b  | backspace
\f  | form feed
\n  | newline
\r  | carriage return
\t  | tab
\o, \oo, \ooo (o = 0 - 7)  | octal byte value
\xh, \xhh (h = 0 - 9, A - F)  | hexadecimal byte value
\uxxxx, \Uxxxxxxxx (x = 0 - 9, A - F)  | 16 or 32-bit hexadecimal Unicode character value


Table 4-2. Operator Precedence (decreasing)
Operator/Element  | Associativity  | Description
--- | --- | ---
.  | left  | table/column name separator
::  | left  | PostgreSQL-style typecast
[ ]  | left  | array element selection
+ -  | right  | unary plus, unary minus
^  | left  | exponentiation
* / %  | left  | multiplication, division, modulo
+ -  | left  | addition, subtraction
IS  |    | IS TRUE, IS FALSE, IS NULL, etc
ISNULL  |    | test for null
NOTNULL  |    | test for not null
(any other)  | left  | all other native and user-defined operators
IN  |    | set membership
BETWEEN  |    | range containment
OVERLAPS  |    | time interval overlap
LIKE ILIKE SIMILAR  |    | string pattern matching
< >  |    | less than, greater than
=  | right  | equality, assignment
NOT  | right  | logical negation
AND  | left  | logical conjunction
OR  | left  | logical disjunction


### 4.2. Value Expressions
https://www.postgresql.org/docs/9.4/sql-expressions.html

Aggregate Functions:  
https://www.postgresql.org/docs/9.4/functions-aggregate.html

### 4.3. Calling Functions
Sample:
```
CREATE FUNCTION concat_lower_or_upper(a text, b text, uppercase boolean DEFAULT false)
RETURNS text
AS
$$
 SELECT CASE
        WHEN $3 THEN UPPER($1 || ' ' || $2)
        ELSE LOWER($1 || ' ' || $2)
        END;
$$
LANGUAGE SQL IMMUTABLE STRICT;
```

Calling:
```
SELECT concat_lower_or_upper('Hello', b := 'World', uppercase := true);
 concat_lower_or_upper 
-----------------------
 HELLO WORLD
(1 row)
```




