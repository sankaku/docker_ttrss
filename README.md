# docker-ttrss
Docker images of RSS reader [Tiny Tiny RSS](https://tt-rss.org) with [full-text RSS converter](https://bitbucket.org/fivefilters/full-text-rss).

These images are
+ nginx  
  Web server
+ MySQL  
  Database for Tiny Tiny RSS
+ Tiny Tiny RSS  
  RSS reader
+ full-text-rss  
  Full-text RSS converter by [FiveFilters.org](http://fivefilters.org/)

## Requirements
+ docker
+ docker-compose(1.13.0+)

## Set up
### Change passwords
You MUST change `MYSQL_ROOT_PASSWORD`(in docker-compose.yml).  
This is the root password of MySQL container.

### Build docker images and run
```sh
$ docker-compose build
$ docker-compose up
```

### Create database for Tiny Tiny RSS
Example below is for setting
+ "Database name" as "ttrssdb"
+ "Username" as "ttrssdbuser"
+ "Password" as "dbpassword"

```
$ docker exec -it ttrss-db-container bash

### Type commands as below in the container
# mysql -u root -p
### Type the changed password(MYSQL_ROOT_PASSWORD)

mysql> create database ttrssdb;
mysql> grant all privileges on ttrssdb.* to ttrssdbuser@localhost identified by 'dbpassword';
mysql> exit
# exit
```

### Install Tiny Tiny RSS
Access `localhost` by your browser and modify "Database settings" section.

+ Database type  
  Choose "MySQL"
+ Username, Password, Database name  
  Fill the blanks as you typed in the "Create database for Tiny Tiny RSS" section.
+ Host name  
  "db"

Then, push "Test configuration", "Initialize database", "Save configuration" and access `localhost` again.  
Login Tiny Tiny RSS(default username and password is `admin` and `password`).

### Restart docker containers
Stop your running `docker-compose up` process by Ctrl-C and execute it again.

This (ridiculous) procedure is needed only once to update feeds.


## Read and subscribe to the full-text RSS
Access `localhost:18888`.  
This is the fivefilters' full-text RSS converter.

To subscribe to the converted RSS on Tiny Tiny RSS, you need to change URL

`http://localhost:18888/makefulltextfeed.php?url=...`

as

`web:18888/makefulltextfeed.php?url=...`


## Acknowledgements
+ [Tiny Tiny RSS](https://tt-rss.org)
+ [FiveFilters.org](http://fivefilters.org/)

## License
MIT License