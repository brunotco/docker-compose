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