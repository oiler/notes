# PostgreSQL

## Install & Setup
```bash
brew update
brew install postgresql
postgres --version
brew services start postgresql
```

```postgres
CREATE ROLE userforpostgres WITH LOGIN PASSWORD 'whateveryouwantforapassword';
ALTER ROLE userforpostgres CREATEDB;
```

```
brew services stop postgresql
```


## Other Commands
```
psql postgres
CREATE DATABASE djangoblog;
CREATE USER postgresuser WITH PASSWORD 'postgresuser';
ALTER ROLE postgresuser SET client_encoding TO 'utf8';
ALTER ROLE postgresuser SET default_transaction_isolation TO 'read committed';
ALTER ROLE postgresuser SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE djangoblog TO postgresuser;
```

```
DROP DATABASE mydatabasename;
```


[source1](https://www.sqlshack.com/setting-up-a-postgresql-database-on-mac/)
[source2](https://www.robinwieruch.de/postgres-sql-macos-setup)


## Table

[data types](https://www.postgresql.org/docs/9.5/datatype.html)

https://www.enterprisedb.com/postgres-tutorials/how-use-postgresql-django