# develop-pool
For develop pool microservices

## set up
First you have to install [docker](https://docs.docker.com/install/) and [docker-compose](https://docs.docker.com/compose/install/).
Then set up the Pool² for developers.
```
  docker-compose up -d
```
It may happen that some dockers do not start properly. This is mostly due to drops and stream trying to reach the database while it is still starting.
Check with `docker ps --filter status=restarting` for restarting dockers. You can simple rebuild docker via `./please reset <serviceName>`.

Next you should initialize the databases. 
```
  ./please initNav && ./please restore drops-database default
```

We save our dumps in the `dumps/` directory. Each database has a folder there. The default dump for each service is named `default.sql`.

## use
# admin
  Email: `admin@pool.org` and password: `admin`
# connect dev server
The pool can be reached at `172.2.20.2`. 
The routes are defined in `routes/nginx-pool/pool2.location` and all upstreams in `routes/nginx-pool/pool2.upstream`. 
There is no way for the Nginx to reach the `localhost` to connect an develop server. 
Therefore, to set up the local development of a service, you need to edit the ip addresses of the service in `routes/nginx-pool/pool2.upstream`.
Find your local external ip address with `ip addr` similar to `192.168.2.34`.
After editing restart nginx via `docker-compose restart nginx-pool`.

# database usage

# docker-compose.yml

# custom navigation

# clean

`docker-compose down`
