# PostgreSQL
## Functions
https://www.postgresql.org/docs/9.4/plpgsql.html


## Difference between MSSQL and PostgreSQL functions  

https://blog.csdn.net/fwxgx_nb/article/details/8730243	

MS SQL 				| PostgreSQL
---    				| ---
@@ROWCOUNT			| DECLARE V_ROW_NUM INT;<br> ... GET DIAGNOSTICS V_ROW_NUM := ROW_COUNT;
@@ERROR				| EXCEPTION<br>WHEN OTHERS THEN<br>RAISE NOTICE 'SQLSTATE: %', SQLSTATE;<br>RAISE NOTICE 'SQLERRM: %', SQLERRM;<br>RETURN SQLSTATE;<br>END;


### Concepts
1. Transaction
Functions and trigger procedures are always executed within a transaction established by an outer query — they cannot start or commit that transaction, since there would be no context for them to execute in. 

However, a block containing an EXCEPTION clause effectively forms a subtransaction that can be rolled back without affecting the outer transaction.


 
### Samples
```
create table myschema.person ( id int, firstname varchar(10), lastname varchar(10), sex boolean, birth timestamp, isvalid boolean);

insert into myschema.person ( id, firstname , lastname , sex , birth , isvalid ) values (1,'John', 'Smith', '1' , '1985-12-08', 'true');
insert into myschema.person ( id, firstname , lastname , sex , birth , isvalid ) values (2,'Jack', 'Simpson', '1' , '1975-2-18', 'true');
insert into myschema.person ( id, firstname , lastname , sex , birth , isvalid ) values (3,'Mary', 'Simpson', '0' , '1975-2-18', 'true');
insert into myschema.person ( id, firstname , lastname , sex , birth , isvalid ) values (2,'Amy', 'Bennet', '0' , '1975-2-18', 'true');
update myschema.person set id=4 where firstname='Amy';

-- IN & OUT
CREATE OR REPLACE FUNCTION prcGetPersonId(
    IN i_firstname character varying
   ,IN i_lastname character varying
  ,OUT o_id integer
)
RETURNS integer AS
$BODY$

BEGIN 
    SELECT id FROM "myschema"."person" WHERE 
    firstname = "i_firstname" AND
    lastname = "i_lastname" INTO o_id;
    RETURN;
END
$BODY$
  LANGUAGE plpgsql;

select prcGetPersonId('John', 'Smith');
 prcgetpersonid 
----------------
              1
(1 row)

```


