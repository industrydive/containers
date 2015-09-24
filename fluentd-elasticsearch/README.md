# Fluentd with the elasticsearch plugin

This docker image adds the elasticsearch plugin and some elasticsearch configuration to the base fluentd docker image.

## Build

````
docker build -t industrydive/fluentd-elasticsearch .
````

## Run
Something like this, except with correct values for `ES_HOST`, `ES_PORT`, `ES_USER`, and `ES_PASSWORD`. This container needs to be started before the others that will log to it. Otherwise docker won't start the othere containers.

````
docker run -d -p 24224:24224 \
-e "ES_HOST=example.com" \
-e "ES_PORT=8080" \
-e "ES_USER=user" \
-e "ES_PASSWORD=secret" \
industrydive/fluentd-elasticsearch
````

For other containers on the same docker host, docker run them with --log-driver=fluentd and docker will send stdout and stderr to localhost:24224 by default, which will be this fluentd container.

## Compatibility
Log driver support was added in docker 1.8.

The `log_driver` can be defined with a docker compose yml file, but not until docker-compose 1.5 comes out. Alternatively, git clone the docker/compose repo and run `sudo python setup.py develop` to get the master version of docker-compose that includes the fluentd support.

