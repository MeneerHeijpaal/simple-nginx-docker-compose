# simple-nginx-docker-compose

This is a simple (*HTTP!!*) nginx deployment with docker-compose. It will serve all the files in the `/data` directory.

## Some explanation
If a file is not found, the server will default to *index.html*.
This can be changed in `/nginx/site/site.conf`

Only GET-requests are allowed, this can also be changed in `/nginx/site/site.conf`

## Deployment
You can set the source and target directories in the `docker-compose.yml`.
```yml
version: '3'

services:
  # The Server 
   nginx:
    image: nginx:1.16.0-alpine
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
      - ./nginx/site/site.conf:/etc/nginx/sites-available/site.conf:ro
      - ./data:/var/www/:ro
    ports:
      - "80:80"
```
Then build and run it in the folder were the `docker-compose.yml` file is located:

    $ docker-compose -f docker-compose.yml up -d
    Creating network "docker_default" with the default driver
    Creating nginx1.16 ... done

## Interact with Docker
You can interact with the Docker image via this command:

    $ docker exec -it nginx1.16 /bin/sh

You can see the output of the Access and Error-log with this command:

    $ docker-compose logs -f
