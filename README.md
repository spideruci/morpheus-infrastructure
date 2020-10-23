# README

Simple configuration for running the test visualization tool. It uses nginx, gunicorn, and flask, where flask and gunicorn are running the backend, while the visualization is served directly from nginx.

## Running the tool

- Prerequisites:
    - Install the following tools:
        - Docker
        - Docker-Compose
    - Optional for debugging:
        - curl

- Install by running the following commands:
```bash
docker-compose build
docker-compose up
```

- To make use of the set up we need to resolve the host `spidertest.org` to the ip address docker is running, which should be 127.0.0.1.
For mac os or linux this can be done by adding the following lines to `/etc/hosts`
```
127.0.0.1       spidertest.org
127.0.0.1       api.spidertest.org
```

After adding the lines to `/etc/hosts/`, we can test if everything is running using curl:
```bash
curl -v http://api.spidertest.org/generate_204
```

It should generate a 204 response as following:
```
> curl -v http://api.spidertest.org/generate_204
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to api.spidertest.org (127.0.0.1) port 80 (#0)
> GET /generate_204 HTTP/1.1
> Host: api.spidertest.org
> User-Agent: curl/7.64.1
> Accept: */*
>
< HTTP/1.1 204 No Content
< Server: nginx/1.19.1
< Date: Sun, 18 Oct 2020 08:16:53 GMT
< Connection: keep-alive
<
* Connection #0 to host api.spidertest.org left intact
* Closing connection 0
```

The backend assumes there will be a database called `research.sqlite` in the root directory of this project, created using the [spidertools](https://github.com/kajdreef/spidertools) project.

## Next steps:
1. Make the following files configurable based on a template (e.g., use jinja to create new template):
    - Make `nginx.conf` configurable for local development and production
    - Make `gunicorn_config.py` configurable for local development and production