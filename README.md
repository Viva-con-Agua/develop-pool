# develop-pool
For develop pool microservices

# set up

## preparation
First you have to install [docker](https://docs.docker.com/install/) and [docker-compose](https://docs.docker.com/compose/install/).

## install
Then set up the Pool² for developers. Docker container will be downloaded and started with:
```
  docker-compose up -d
```
NOTE: It may happen that some dockers do not start properly. 
This is mostly due to drops and stream trying to reach the database while it is still starting.
Check state of the docker containers with `docker ps --filter status=restarting` for restarting dockers. 
If there are some containers shown to be restarting, you can simple rebuild these docker via `./please reset <serviceName>`.

Next you should initialize the navigation and the user database. 
```
  ./please initNav && ./please restore drops-database default
```
We save our dumps in the `dumps/` directory. Each database has a folder there. The default dump for each service is named `default.sql`.

# usage

## connect dev server
The pool can be reached at `172.2.20.2`.

## admin
  Username: `admin@pool.org`
  Password: `admin`

## local development
The routes are defined in `routes/nginx-pool/pool2.location` and all upstreams in `routes/nginx-pool/pool2.upstream`. 
There is no way for the Nginx to reach the `localhost` to connect an develop server. 
Therefore, to set up the local development of a service, you need to edit the ip addresses of the service in `routes/nginx-pool/pool2.upstream`.
Find your local external ip address with `ip addr` similar to `192.168.2.34`.
After editing restart nginx via `docker-compose restart nginx-pool`.

## database usage

To connect to the database, you can run `docker exec -it <docker-container> mysql -u <db-user> -p` and use the default password.
For example: To connect to the user database of drops run `docker exec -it drops-database mysql -u drops -p` and use the default password.

# docker-compose.yml

The file `docker-compose.yml` describes the names, ip addresses and docker container of all services, that should be running on the server.

# useful docker commands
  Show the current docker network with `docker inspect developpool_pool-network`
  Enter docker container bash with `docker exec -it <docker-container> bash`
  Show logs of docker container with `docker logs <docker-container>`

# custom navigation

# clean

`docker-compose down`
