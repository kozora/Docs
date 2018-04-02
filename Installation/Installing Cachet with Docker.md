---
title: "Installing Cachet with Docker"
excerpt: ""
---
[block:callout]
{
  "type": "success",
  "title": "Thank you, community!",
  "body": "Docker support is maintained by Cachet users from within the community."
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Getting started with Docker Compose"
}
[/block]
Quickly launch Cachet, NGINX and PostgreSQL docker images with [docker-compose](https://docs.docker.com/compose/).   

1. Clone the repository:
[block:code]
{
  "codes": [
    {
      "code": "$ git clone https://github.com/cachethq/Docker.git cachet-docker\n$ cd cachet-docker",
      "language": "shell"
    }
  ]
}
[/block]
2. Edit the docker-compose.yml file to specify your [ENV variables](https://github.com/CachetHQ/Docker/blob/master/conf/.env.docker).

3. To build an image containing a specific [Cachet release](https://github.com/CachetHQ/Cachet/releases), change the [`cachet_ver` ARG in the docker-compose.yml](https://github.com/CachetHQ/Docker/blob/master/docker-compose.yml) file:
[block:code]
{
  "codes": [
    {
      "code": "  cachet:\n    build:\n      context: .\n      args:\n        - cachet_ver=v2.3.10",
      "language": "yaml"
    }
  ]
}
[/block]
4. Build and run the image:
[block:code]
{
  "codes": [
    {
      "code": "$ docker-compose build\n$ docker-compose up",
      "language": "shell"
    }
  ]
}
[/block]
5. Continue to configure Cachet in your web browser by navigating to your Docker host's IP address.
[block:callout]
{
  "type": "success",
  "body": "**cachethq/docker** runs on port 8000 by default. This is exposed on host port 80 when using docker-compose.",
  "title": "Default port"
}
[/block]

[block:callout]
{
  "type": "warning",
  "body": "The *master* branch and \"cachethq/docker:latest\" Docker automated build are a work in progress / development version of the upstream https://github.com/CachetHQ/Cachet project. As such, *master* or *latest* should not be used in a production environment as it may change at anytime.\n\nWe strongly recommend specifying a stable [Cachet Release](https://github.com/CachetHQ/Cachet/releases) at build time as mentioned in step 3 above.",
  "title": "Version stability warning:"
}
[/block]

[block:callout]
{
  "type": "danger",
  "body": "This is commonly achieved by running Nginx with your certificates on your Docker host, service or load balancers in-front of the running container, or by adding your custom SSL certificates and configuration to the supplied Nginx configuration.",
  "title": "When running in production you should ensure that you enable SSL."
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Running Cachet Docker container manually"
}
[/block]
Run a DB container:
[block:code]
{
  "codes": [
    {
      "code": "$ docker run --name postgres -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -d postgres:9.5",
      "language": "shell"
    }
  ]
}
[/block]
Run Cachet:
[block:code]
{
  "codes": [
    {
      "code": "$ docker run -d --name cachet --link postgres -e DB_DRIVER=pgsql -e DB_HOST=postgres -e DB_DATABASE=postgres -e DB_USERNAME=postgres -e DB_PASSWORD=postgres -d cachethq/docker:latest",
      "language": "shell"
    }
  ]
}
[/block]
Now go to `http://<ipdockerisboundto>:8000/setup` and have fun!