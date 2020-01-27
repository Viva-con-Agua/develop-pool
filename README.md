# develop-pool
For develop pool microservices

## use
install docker-compose
# start
run `docker-compose up -d`
the first time the network is started, account and oauthclients must be created. (script follows)

# setup dev

`nginx-pool` needs a route to your dev server. These are set up in `volume/nginx-pool/conf/pool2.upstream`
uses the external ip of your home network. Not localhost!! 
if `pool2.upstream` is set, you have to restart the `nginx-pool`.
`docker-compose restart nginx-pool`


# clean

`docker-compose down`

# more
https://docs.docker.com/compose/compose-file/
