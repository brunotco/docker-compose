# Docker Compose
Docker compose files for running application stacks.

# Usage
The Docker Compose files can be used with just plain Docker (using Docker Compose), but I prefer to use them with `Portainer`, see Portainer section.

If the prefered usage is plain Docker Compose command, you need a file named `docker-compose.yml` and on the file directory run:
```
docker compose up -d
```

The `-d` flag will run the container in the background.

The variables present in the compose files `${VARIABLE}` use environment variables defined in `.env` file in the root directory of the `docker-compose.yml` or, if using `Portainer`, it uses environment variables defined on the Stack itself.

# Notes

## Run outside Portainer
There are two containers that shouldn't be runned from within `Portainer`, and should be started from command line.
`Portainer` itself, obviously since it needs to be running to make a container run from it.
`Traefik` because, since it works as a reverse proxy and points to services, it needs to be running to access services like `Portainer`.

## Required with Traefik
Compose files might contain a `Required with Traefik` section, this is only required if using `Traefik` as reverse proxy, so you can delete this parts if not using it and uncomment the commented ports to expose the container ports on the host.