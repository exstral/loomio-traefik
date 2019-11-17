I wanted to use traefik to host my own instance of loomio, so started working on this simplified variant of https://github.com/loomio/loomio-deploy.

# Prerequisites
You need something that automatically forwards all .test domains to localhost so that `app.loomio.test` ends up on your local machine and can be routed by traefik to the container.

Here is a guide on how to set it up: https://exstral.eu/2019/11/17/local-development-test-domain/


# Initial Setup
Create your .env file using provided example.
```
cp .env.example .env
```

Initialize the db on first run before you do a normal docker-compose up.
TODO: Would love to make this initial setup automatic somehow.
```
docker-compose up -d loomio-db
# Wait some seconds for the container to start properly
docker-compose run loomio-app rake db:setup
# Start the rest of the containers
docker-compose up
```

Next time you can directly start all containers with `docker-compose up`. 

Access your local loomio app on http://app.loomio.test

Traefik dashboard can be found at http://localhost:8080


# Known issues
Services start properly but all pages are empty white :(