

list users
SELECT User, Host, Password FROM mysql.user;

lists dbs
SELECT SCHEMA_NAME AS `Database` FROM INFORMATION_SCHEMA.SCHEMATA


* alias table name
`SELECT p.last_name FROM person p;`

* multiple select
`SELECT p.first_name, p.last_name FROM person p;`

* where clause
`SELECT p.last_name FROM person p WHERE p.first_name='Jon';`

* operators
`= <> > < >= <= between like in is isnot`

* operator clause examples
`SELECT p.last_name FROM person p WHERE p.first_name='Jon' AND p.age>35;`
`SELECT p.last_name FROM person p WHERE p.first_name='Jon' OR p.last_name='Snow';`
`SELECT p.first_name, p.last_name FROM person p WHERE p.age BETWEEN 18 AND 35;`
`SELECT p.first_name, p.last_name FROM person p WHERE p.first_name LIKE 'J%';`
`SELECT p.first_name, p.last_name FROM person p WHERE p.first_name IN ('Jon','Ned','Rob');`
`SELECT p.first_name, p.last_name FROM person p WHERE p.first_name IS NULL;`
`SELECT p.first_name, p.last_name FROM person p WHERE p.first_name IS NOT NULL;`

* set functions
`COUNT MAX MIN AVG SUM`

* working with results
`SELECT p.first_name, p.last_name FROM person p ORDER BY p.last_name;`
`SELECT SUM(p.wins) FROM person p;`
`SELECT AVG(p.age) FROM person p;`
`SELECT COUNT(DISTINCT p.house_name) FROM person p;`
`SELECT COUNT(DISTINCT p.house_name), p.house_name FROM person p GROUP BY p.house_name;`
`SELECT COUNT(DISTINCT p.last_name), p.last_name FROM person p GROUP BY p.last_name HAVING COUNT(DISTINCT p.last_name) >=2;`

* joins
bad, cross join = `SELECTION p.first_name, f.mother FROM person p, family f;`
ignore nulls, inner join = `SELECTION p.first_name, p.last_name, m.weapon FROM person p INNER JOIN meta m ON p.id = m.pid;`
include nulls, left outer join = `SELECTION p.first_name, p.last_name, m.weapon FROM person p LEFT OUTER JOIN meta m ON p.id = m.pid;`
include nulls, right outer join = `SELECTION p.first_name, p.last_name, m.weapon FROM person p RIGHT OUTER JOIN meta m ON p.id = m.pid;`
full outer join = not supported by mysql

* crud
`INSERT INTO person (first_name, last_name) VALUES ('arya', 'stark');`
`INSERT INTO person p SELECT * FROM old_person op WHERE op.id > 100;`
`UPDATE person p SET p.last_name = 'Targaryen' WHERE p.first_name='Jon' AND p.last_name='Snow';`
`DELETE FROM person p WHERE p.first_name='Petyr' AND p.last_name='Baelish';`





