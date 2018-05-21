---
title: Some tips about PostgreSQL and MIMICIII database
categories: Databases
abbrlink: 59269
date: 2017-01-13 21:40:15
tags:
  - PostgreSQL
  - MIMICIII
---
## Intro to PostgreSQL

### Architectural Fundamentals

PostgreSQL uses a client/server model. A PostgreSQL session consists of the following cooperating processes (programs):

1. A server process, which manages the database files, accepts connections to the database from client applications, and performs database actions on behalf of the clients. The database server program is called postgres.

2. The user's client (frontend) application that wants to perform database operations. Client applications can be very diverse in nature: a client could be a text-oriented tool, a graphical application, a web server that accesses the database to display web pages, or a specialized database maintenance tool. Some client applications are supplied with the PostgreSQL distribution; most are developed by users.

The PostgreSQL server can handle multiple concurrent connections from clients. To achieve this it starts ("forks") a new process for each connection. From that point on, the client and the new server process communicate without intervention by the original postgres process. Thus, the master server process is always running, waiting for client connections, whereas client and associated server processes come and go. (All of this is of course invisible to the user. We only mention it here for completeness.)

### Concepts

PostgreSQL is a relational database management system (RDBMS). That means it is a system for managing data stored in relations. Relation is essentially a mathematical term for table. The notion of storing data in tables is so commonplace today that it might seem inherently obvious, but there are a number of other ways of organizing databases. Files and directories on Unix-like operating systems form an example of a hierarchical database. A more modern development is the object-oriented database.

1. Each table is a named collection of rows. Each row of a given table has the same set of named columns, and each column is of a specific data type. Whereas columns have a fixed order in each row, it is important to remember that SQL does not guarantee the order of the rows within the table in any way (although they can be explicitly sorted for display).

2. Tables are grouped into databases, and a collection of databases managed by a single PostgreSQL server instance constitutes a database cluster.

### Creating a New Table

You can create a new table by specifying the table name, along with all column names and their types:

```sql
CREATE TABLE weather (
    city            varchar(80),
    temp_lo         int,           -- low temperature
    temp_hi         int,           -- high temperature
    prcp            real,          -- precipitation
    date            date
);
```

You can enter this into psql with the line breaks. psql will recognize that the command is not terminated until the semicolon.
White space (i.e., spaces, tabs, and newlines) can be used freely in SQL commands. That means you can type the command aligned differently than above, or even all on one line. Two dashes ("--") introduce comments. Whatever follows them is ignored up to the end of the line. SQL is case insensitive about key words and identifiers, except when identifiers are double-quoted to preserve the case (not done above).
varchar(80) specifies a data type that can store arbitrary character strings up to 80 characters in length. int is the normal integer type. real is a type for storing single precision floating-point numbers. date should be self-explanatory. (Yes, the column of type date is also named date. This might be convenient or confusing — you choose.)
PostgreSQL supports the standard SQL types int, smallint, real, double precision, char(N), varchar(N), date, time, timestamp, and interval, as well as other types of general utility and a rich set of geometric types. PostgreSQL can be customized with an arbitrary number of user-defined data types. Consequently, type names are not key words in the syntax, except where required to support special cases in the SQL standard.
The second example will store cities and their associated geographical location:

```sql
CREATE TABLE cities (
    name            varchar(80),
    location        point
);
```

The point type is an example of a PostgreSQL-specific data type.
Finally, it should be mentioned that if you don't need a table any longer or want to recreate it differently you can remove it using the following command:

```sql
DROP TABLE tablename;
```

### Populating a Table With Rows

The INSERT statement is used to populate a table with rows:

```sql
INSERT INTO weather VALUES ('San Francisco', 46, 50, 0.25, '1994-11-27');
```

Note that all data types use rather obvious input formats. Constants that are not simple numeric values usually must be surrounded by single quotes ('), as in the example. The date type is actually quite flexible in what it accepts, but for this tutorial we will stick to the unambiguous format shown here.
The point type requires a coordinate pair as input, as shown here:

```sql
INSERT INTO cities VALUES ('San Francisco', '(-194.0, 53.0)');
```

The syntax used so far requires you to remember the order of the columns. An alternative syntax allows you to list the columns explicitly:

```sql
INSERT INTO weather (city, temp_lo, temp_hi, prcp, date)
    VALUES ('San Francisco', 43, 57, 0.0, '1994-11-29');
```

You can list the columns in a different order if you wish or even omit some columns, e.g., if the precipitation is unknown:

```sql
INSERT INTO weather (date, city, temp_hi, temp_lo)
    VALUES ('1994-11-29', 'Hayward', 54, 37);
```

Many developers consider explicitly listing the columns better style than relying on the order implicitly.
Please enter all the commands shown above so you have some data to work with in the following sections.
You could also have used COPY to load large amounts of data from flat-text files. This is usually faster because the COPY command is optimized for this application while allowing less flexibility than INSERT. An example would be:

```sql
COPY weather FROM '/home/user/weather.txt';
```

where the file name for the source file must be available on the machine running the backend process, not the client, since the backend process reads the file directly. You can read more about the COPY command in COPY.

### Using SELECT

Querying a Table
To retrieve data from a table, the table is queried. An SQL SELECT statement is used to do this. The statement is divided into a select list (the part that lists the columns to be returned), a table list (the part that lists the tables from which to retrieve the data), and an optional qualification (the part that specifies any restrictions). For example, to retrieve all the rows of table weather, type:

```sql
SELECT * FROM weather;
```

Here * is a shorthand for "all columns". So the same result would be had with:

```sql
SELECT city, temp_lo, temp_hi, prcp, date FROM weather;
```

You can write expressions, not just simple column references, in the select list. For example, you can do:

```sql
SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, date FROM weather;
```

A query can be "qualified" by adding a WHERE clause that specifies which rows are wanted. The WHERE clause contains a Boolean (truth value) expression, and only rows for which the Boolean expression is true are returned. The usual Boolean operators (AND, OR, and NOT) are allowed in the qualification. For example, the following retrieves the weather of San Francisco on rainy days:

```sql
SELECT * FROM weather
    WHERE city = 'San Francisco' AND prcp > 0.0;
```

You can request that the results of a query be returned in sorted order:

```sql
SELECT * FROM weather
    ORDER BY city;
```

In this example, the sort order isn't fully specified, and so you might get the San Francisco rows in either order. But you'd always get the results shown above if you do:

```sql
SELECT * FROM weather
    ORDER BY city, temp_lo;
```

You can request that duplicate rows be removed from the result of a query:

```sql
SELECT DISTINCT city
    FROM weather;
```

Here again, the result row ordering might vary. You can ensure consistent results by using DISTINCT and ORDER BY together:

```sql
SELECT DISTINCT city
    FROM weather
    ORDER BY city;
```

### Joins Between Tables

Thus far, our queries have only accessed one table at a time. Queries can access multiple tables at once, or access the same table in such a way that multiple rows of the table are being processed at the same time. A query that accesses multiple rows of the same or different tables at one time is called a join query. As an example, say you wish to list all the weather records together with the location of the associated city. To do that, we need to compare the city column of each row of the weather table with the name column of all rows in the cities table, and select the pairs of rows where these values match.
This would be accomplished by the following query:

```sql
SELECT *
    FROM weather, cities
    WHERE city = name;
```

Observe two things about the result set:

There is no result row for the city of Hayward. This is because there is no matching entry in the cities table for Hayward, so the join ignores the unmatched rows in the weather table. We will see shortly how this can be fixed.

There are two columns containing the city name. This is correct because the lists of columns from the weather and cities tables are concatenated. In practice this is undesirable, though, so you will probably want to list the output columns explicitly rather than using \*:

```sql
SELECT city, temp_lo, temp_hi, prcp, date, location
    FROM weather, cities
    WHERE city = name;
Exercise: Attempt to determine the semantics of this query when the WHERE clause is omitted.
```

Since the columns all had different names, the parser automatically found which table they belong to. If there were duplicate column names in the two tables you'd need to qualify the column names to show which one you meant, as in:

```sql
SELECT weather.city, weather.temp_lo, weather.temp_hi,
       weather.prcp, weather.date, cities.location
    FROM weather, cities
    WHERE cities.name = weather.city;
```

It is widely considered good style to qualify all column names in a join query, so that the query won't fail if a duplicate column name is later added to one of the tables.

Join queries of the kind seen thus far can also be written in this alternative form:

```sql
SELECT *
    FROM weather INNER JOIN cities ON (weather.city = cities.name);
```

This syntax is not as commonly used as the one above, but we show it here to help you understand the following topics.

Now we will figure out how we can get the Hayward records back in. What we want the query to do is to scan the weather table and for each row to find the matching cities row(s). If no matching row is found we want some "empty values" to be substituted for the cities table's columns. This kind of query is called an outer join. (The joins we have seen so far are inner joins.) The command looks like this:

```sql
SELECT *
    FROM weather LEFT OUTER JOIN cities ON (weather.city = cities.name);
```

This query is called a left outer join because the table mentioned on the left of the join operator will have each of its rows in the output at least once, whereas the table on the right will only have those rows output that match some row of the left table. When outputting a left-table row for which there is no right-table match, empty (null) values are substituted for the right-table columns.

Exercise: There are also right outer joins and full outer joins. Try to find out what those do.

We can also join a table against itself. This is called a self join. As an example, suppose we wish to find all the weather records that are in the temperature range of other weather records. So we need to compare the temp_lo and temp_hi columns of each weather row to the temp_lo and temp_hi columns of all other weather rows. We can do this with the following query:

```sql
SELECT W1.city, W1.temp_lo AS low, W1.temp_hi AS high,
    W2.city, W2.temp_lo AS low, W2.temp_hi AS high
    FROM weather W1, weather W2
    WHERE W1.temp_lo < W2.temp_lo
    AND W1.temp_hi > W2.temp_hi;
```

Here we have relabeled the weather table as W1 and W2 to be able to distinguish the left and right side of the join. You can also use these kinds of aliases in other queries to save some typing, e.g.:

```sql
SELECT *
    FROM weather w, cities c
    WHERE w.city = c.name;
You will encounter this style of abbreviating quite frequently.
```

### Aggregate Functions

Like most other relational database products, PostgreSQL supports aggregate functions. An aggregate function computes a single result from multiple input rows. For example, there are aggregates to compute the count, sum, avg (average), max (maximum) and min (minimum) over a set of rows.
As an example, we can find the highest low-temperature reading anywhere with:

```sql
SELECT max(temp_lo) FROM weather;
```

If we wanted to know what city (or cities) that reading occurred in, we might try:

```sql
SELECT city FROM weather WHERE temp_lo = max(temp_lo);     WRONG
```

but this will not work since the aggregate max cannot be used in the WHERE clause. (This restriction exists because the WHERE clause determines which rows will be included in the aggregate calculation; so obviously it has to be evaluated before aggregate functions are computed.) However, as is often the case the query can be restated to accomplish the desired result, here by using a subquery:

```sql
SELECT city FROM weather
    WHERE temp_lo = (SELECT max(temp_lo) FROM weather);
```

This is OK because the subquery is an independent computation that computes its own aggregate separately from what is happening in the outer query.
Aggregates are also very useful in combination with GROUP BY clauses. For example, we can get the maximum low temperature observed in each city with:

```sql
SELECT city, max(temp_lo)
    FROM weather
    GROUP BY city;
```

which gives us one output row per city. Each aggregate result is computed over the table rows matching that city. We can filter these grouped rows using HAVING:

```sql
SELECT city, max(temp_lo)
    FROM weather
    GROUP BY city
    HAVING max(temp_lo) < 40;
```

which gives us the same results for only the cities that have all temp_lo values below 40. Finally, if we only care about cities whose names begin with "S", we might do:

```sql
SELECT city, max(temp_lo)
    FROM weather
    WHERE city LIKE 'S%'(1)
    GROUP BY city
    HAVING max(temp_lo) < 40;
```

It is important to understand the interaction between aggregates and SQL's WHERE and HAVING clauses. The fundamental difference between WHERE and HAVING is this: WHERE selects input rows before groups and aggregates are computed (thus, it controls which rows go into the aggregate computation), whereas HAVING selects group rows after groups and aggregates are computed. Thus, the WHERE clause must not contain aggregate functions; it makes no sense to try to use an aggregate to determine which rows will be inputs to the aggregates. On the other hand, the HAVING clause always contains aggregate functions. (Strictly speaking, you are allowed to write a HAVING clause that doesn't use aggregates, but it's seldom useful. The same condition could be used more efficiently at the WHERE stage.)
In the previous example, we can apply the city name restriction in WHERE, since it needs no aggregate. This is more efficient than adding the restriction to HAVING, because we avoid doing the grouping and aggregate calculations for all rows that fail the WHERE check.

### Updates

You can update existing rows using the UPDATE command. Suppose you discover the temperature readings are all off by 2 degrees after November 28. You can correct the data as follows:

```sql
UPDATE weather
    SET temp_hi = temp_hi - 2,  temp_lo = temp_lo - 2
    WHERE date > '1994-11-28';
```

Look at the new state of the data:

```sql
SELECT * FROM weather;
```

### Deletions

Rows can be removed from a table using the DELETE command. Suppose you are no longer interested in the weather of Hayward. Then you can do the following to delete those rows from the table:

```sql
DELETE FROM weather WHERE city = 'Hayward';
```

All weather records belonging to Hayward are removed.

```sql
SELECT * FROM weather;
```

One should be wary of statements of the form

```sql
DELETE FROM tablename;
```

Without a qualification, DELETE will remove all rows from the given table, leaving it empty. The system will not request confirmation before doing this!

## Creating a MIMIC III Database

After installation refers to [PostgreSQL download](https://www.postgresql.org/download), then create a database role "mimicuser" to access the data

```bash
sudo -u postgres -i
createuser -P -s -e -d mimicuser
```

Connect to the database with psql

```bash
psql -U postgres -d postgres
```

Create an empty database containing a MIMIC-III schema whose database role is "mimicuser"

```sql
=# CREATE DATABASE mimic OWNER mimicuser;
```

Create a schema to hold the data

```sql
=# \c mimic;
=# CREATE SCHEMA mimiciii;
=# set search_path to mimiciii;
```

Note that after doing this, you have to type 'set search_path to mimiciii;' everytime you wanna connect to the database.

Set the password for 'postgres' and 'mimicuser'

```sql
\password postgres
\password mimicuser
```

Enter a password, to avoid memorization issues here I use 'password' as the password.
To allow password identification, we have to change the'hab_file', use following command to get the file path:

```sql
=# show hba_file;
=# show config_file;
```

In my system the path is /etc/postgresql/9.6/main/pg_hba.conf

```bash
vim /etc/postgresql/9.6/main/pg_hba.conf
```

Change the local all all from peer to md5 to allow password identification for 'mimicuser'.

```bash
Database administrative login by Unix domain socket
local   all             postgres                                peer
TYPE  DATABASE        USER            ADDRESS                 METHOD
"local" is for Unix domain socket connections only
local   all             all                          "peer" to "md5"
IPv4 local connections:
host    all             all             127.0.0.1/32            md5
IPv6 local connections:
host    all             all             ::1/128                 md5
```

Restart PostgreSQL

```bash
sudo service postgresql restart
```

After restart of the postgresql service, now I can use 'mimicuser' and its password to access the database.

```bash
psql -U mimicuser -d mimic
```

Create a set of empty tables on a mimiciii schema, ready to populate with the data

```bash
psql 'dbname=mimic user=mimicuser options=--search_path=mimiciii' -f postgres_create_tables.sql
```

Import the CSV data files into the empty tables

```bash
psql 'dbname=mimic user=mimicuser options=--search_path=mimiciii' -f postgres_load_data.sql -v mimic_data_dir='<path_to_data>'
```

Indexes provide additional structure for the database that can help to improve the speed of queries. The MIMIC code repository includes a script with a set of suggested indexes. As before, you can run this script from the command line to add indexes to improve performance

```bash
psql 'dbname=mimic user=mimicuser options=--search_path=mimiciii' -f postgres_add_indexes.sql
```

Run checks, We have included a script which verifies all rows have been loaded in. Run those checks now

```bash
psql 'dbname=mimic user=mimicuser options=--search_path=mimiciii' -f postgres_checks.sql
```

MIMIC-III is ready for analysis

You should now have a working copy of MIMIC-III ready to query with the psql command line tool. First start the PSQL client from the command line:

```bash
psql 'dbname=mimic user=mimicuser options=--search_path=mimiciii'
```

Before going further, you should grant all privileges needed to the mimic user, then revoke the superuser privilege:

```sql
grant select on all tables in schema mimiciii to mimicuser;
grant usage on schema mimiciii to mimicuser;
grant connect on database mimic to mimicuser;
alter user mimicuser nosuperuser;
```

Now try, for example, counting the number of patients in the database:

```sql
select count(subject_id)
from mimiciii.patients;
```

string above (--search_path=mimiciii), we can omit it in the query:

```sql
select count(subject_id)
from patients;
```

Install a graphical user interface

[pgAdmin](https://www.pgadmin.org/)
[Navicat](https://www.navicat.com/)
[DataGrip](https://www.jetbrains.com/datagrip/)
