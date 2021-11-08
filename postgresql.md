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
CREATE DATABASE mydatabasename;
DROP DATABASE mydatabasename;
```


[source1](https://www.sqlshack.com/setting-up-a-postgresql-database-on-mac/)
[source2](https://www.robinwieruch.de/postgres-sql-macos-setup)