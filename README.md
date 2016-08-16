# Cinema - Example of Microservices in Go with Docker and MongoDB

Overview
========

Cinema is an example project which demonstrates the use of microservices for a fictional movie theater.
The Cinema backend is powered by 4 microservices, all of witch happen to be written in Go, using MongoDB for manage the database and Docker to isolate and deploy the ecosystem.

 * Movie Service: Provides information like movie ratings, title, etc.
 * Show Times Service: Provides show times information.
 * Booking Service: Provides booking information. 
 * Users Service: Provides movie suggestions for users by communicating with other services.

The Cinema use case is based on the project written in Python .... by ...
The proyect structure is based in the knowledge learned in the book: Web
Development with Go by Shiju Varghese, ISBN 978-1-4842-1053-6

Requirements
===========

* Docker 1.12
* Docker Compose 1.8

We must **add virtual domains** in order to use each **api entry point**. By default we are using: **movies.local**, **bookings.local**, **users.local** and **showtimes.local**

**Virtual domains** has been defined in `docker-compose.yml` file and configured in `/etc/hosts` file. Example of `/etc/hosts` file:

```
127.0.0.1   movies.local, bookings.local, users.local, showtimes.local
```

Starting Services
==============================

```
docker-compose up -d
```

Restore database information
======================

You can start using an empty database for all microservices, but if you want you can restore a preconfigured data following this steps:

Access to mongodb container typing:
```
docker exec -it cinema-db /bin/bash
```

Restore data typing:
```
/backup/restore.sh
```

Leave the container:
```
exit
```


Documentation
======================

## User Service

This service returns information about the users of Cinema 3.

**_Routes:_**

* GET - http://users.local/users : Get all users
* POST - http://users.local/users : Create user
* DELETE - http://users.local/users/{id} : Remove user by id

## Movie Service

This service is used to get information about a movie. It provides the movie title, rating on a 1-10 scale, director and other information.

**_Routes:_**

* GET - http://movies.local/movies : Get all movies
* POST - http://movies.local/movies : Create movie
* GET - http://movies.local/movies/{id} : Get movie by id
* DELETE - http://movies.local/movies/{id} : Remove movie by id

## Showtimes Service

This service is used get a list of movies playing on a certain date.

**_Routes:_**

* GET - http://showtimes.local/showtimes : Get all showtimes
* POST - http://showtimes.local/showtimes : Create showtime
* GET - http://showtimes.local/showtimes/{id} : Get showtime by id
* DELETE - http://showtimes.local/showtimes/{id} : Remove showtime by id

## Booking Service

**_Routes:_**

Used to lookup booking information for users.

