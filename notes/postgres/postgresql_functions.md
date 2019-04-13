https://blog.csdn.net/fwxgx_nb/article/details/8730243


create table myschema.person ( id int, firstname varchar(10), lastname varchar(10), sex boolean, birth timestamp, isvalid boolean);

insert into myschema.person ( id, firstname , lastname , sex , birth , isvalid ) values (1,'John', 'Smith', '1' , '1985-12-08', 'true');
insert into myschema.person ( id, firstname , lastname , sex , birth , isvalid ) values (2,'Jack', 'Simpson', '1' , '1975-2-18', 'true');
insert into myschema.person ( id, firstname , lastname , sex , birth , isvalid ) values (3,'Mary', 'Simpson', '0' , '1975-2-18', 'true');
insert into myschema.person ( id, firstname , lastname , sex , birth , isvalid ) values (2,'Amy', 'Bennet', '0' , '1975-2-18', 'true');
update myschema.person set id=4 where firstname='Amy';



