# test-db-pg-dvdrental
PostgreSQL DVD Rental database very useful to test purposes and playing with queries.

The idea was to create Docker image containing ready to use database example with sample data. 
I used sample database from PostgreSQL Tutorial and created Dockerfile to run postgres and restore db from backup.
 
 
## Useful links
- [Docker documentation](https://docs.docker.com/)
- [Postgres image](https://hub.docker.com/_/postgres/)
- [PostgreSQL Tutorial](http://www.postgresqltutorial.com/postgresql-sample-database/)

## PostgreSQL Tutorial ER Diagram
![PostgreSQL Tutorial DVD Rental ER Diagram](er_diagram.png)



## Building docker image
First of all we have to build docker image. We can do it by execute:
```docker
docker build -t pg_dvdrental .
```
Docker will download all needed dependencies and build image with name "pg_dvdrental". We can check it by execute:
```docker
docker images
```


## Running docker container
To run created image we have to execute "docker run" like this:
```docker
docker run -p 5433:5432 --name dvdrental -d pg_dvdrental
```
Docker will run container with name "dvdrental", based on image "pg_dvdrental" and it will expose containers port 5432 on localhost port 5433.



## Connect to database
Now we can connect to our database. First we need credentials:
```
Database name: dvdrental
Database user: dvdrental
Database password: dvdrental
```

So lets check it using "docker" and "psql":
```docker
docker run -it --rm --link dvdrental:postgres postgres psql -h postgres -U dvdrental -d dvdrental
```
After put password ("dvdrental" to remind) we are connected to database and we can do queries. Let's 

```docker
docker run -it --rm --link dvdrental:postgres postgres psql -h postgres -U dvdrental -d dvdrental
```

and then:
```postgresql
SELECT * FROM actor WHERE first_name ilike 'Kevin';
```
