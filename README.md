# Star Wars Data
This repository contains a simple multi-purpose data set for PostgreSQL database. Feel free to reuse it to bootstrap your projects.

# Data Model
This data set is composed of two tables:
* `planet`: List of planets appearing in Star Wars movies (**61 records**)
* `people`: List of people appearing in Star Wars movies (**87 records**)

There is a relationship between planets and people as one planet is the homeworld of one or several persons. It is a "one-to-many" relationship (one planet, many people). The `planet_id` column in the `people` table is a foreign key of the `planet` table.

![Data Model](https://github.com/alexisrolland/star-wars-data/blob/master/data_model.png)

# How To
* Connect to your PostgreSQL database server with the client of your choice
* Copy SQL statements from the file [database.sql](https://github.com/alexisrolland/star-wars-data/blob/master/database.sql)
* Execute SQL statements, they will do the following:
  * Create a new database named `star_wars`
  * Create a new schema named `base`
  * Create `planet` and `people` tables
  * Insert data into both tables

# Queries Examples
Count number of planets:
```
\connect star_wars;
select count(*) from base.planet;

 count 
-------
    61
(1 row)
```

Find the Skywalker family:
```
\connect star_wars;
select a.name as character, b.name as planet
from base.people a
inner join base.planet b on a.planet_id=b.id
where a.name like '%Skywalker%';

    character     |  planet  
------------------+----------
 Shmi Skywalker   | Tatooine
 Anakin Skywalker | Tatooine
 Luke Skywalker   | Tatooine
(3 rows)
```

# Copyrights
Star Wars and all associated names are copyrighted by Lucasfilm ltd.

All data has been collected from the open source website [Star Wars API](https://swapi.co).
