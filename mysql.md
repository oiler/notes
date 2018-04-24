

list users
SELECT User, Host, Password FROM mysql.user;

lists dbs
SELECT SCHEMA_NAME AS `Database` FROM INFORMATION_SCHEMA.SCHEMATA
