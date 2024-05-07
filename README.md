# Docker Guide

## Manipulating Docker Images With Docker Client

- List docker images locally:
    ```
    docker images
    ```

- List all the containers:
    ```
    docker ps
    docker ps -a
    docker ps -all
    ```

- Create new image:
    ```
    docker create dockerImage
    ```

- Start the image:
    ```
    docker start dockerImage
    ```

- Docker run will create and start a container:
    ```
    docker run dockerImage
    ```

- Start and print standar output:
    ```
    docker start -a containerId
    ```

- Remove local containers:
    ```
    docker system prune
    ```

- Print container logs:
    ```
    docker logs containerId
    ```

- Stop a container (using sigterm message, giving time to the programs to stop):
    ```
    docker stop containerId
    ```
    or using kill, shutdown immediatelly:
    ```
    socker kill containerId
    ```

- Execute a program/cmd (can be a shell (sh)) inside a running container:
    ```
    docker exec containerId program/cmd
    ```
    if want to open the terminal interactive(STDIN/STDOUT):
    ```
    docker exec -it containerId program/cmd
    ```
    only STDIN:
    ```
    docker exec -i containerId program/cmd
    ```
    only STDOUT:
    ```
    docker exec -t containerId program/cmd
    ```

- Run shell inside an image:
    ```
    docker run -it image sh
    ```

## Build Custom Images

- Buildkit Notes:
    - Buildkit will hide away much of its progress which is something the legacy builder did not do. To see this output, you will want to pass the progress flag to the build command:
        ```
        docker build --progress=plain .
        ```

    - Additionally, you can pass the no-cache flag to disable any caching:
        ```
        docker build --no-cache --progress=plain .
        ```

    - To disable Buildkit, you can just pass the following variable to the build command:
        ```
        DOCKER_BUILDKIT=0 docker build .
        ```

- Using a Dockerfile placed on the working directory:
    ```
    docker build .
    ```

- Create a tagged image:
    ```
    docker build -t dockerId/repoorprojectname:version .
    ```

- Launch docker tagged image:
    ```
    docker run -t dockerId/repoorprojectname
    ```
    or 
    ```
    docker run -t dockerId/repoorprojectname:version
    ```

- Commit docker container changes after executing some commands into a new docker image and put a cmd at startup:
    ```
    docker commit -c 'CMD ["commandhere"]' runingcontainerId
    ```
- Container ports:
    ```
    docker run -p localhostport:containerport imagename
    ```

- Delete a container:
    ```
    docker rm containerId
    ```

- Delete an image:
    ```
    docker images rm imageId
    ```

- Run a container with a shell command:
    ```
    docker run -it dockerId/repoorprojectname sh
    ```

- Run a shell in an existing running container:
    ```
    docker exec -it containerId sh
    ```

## Docker compose

- Docker compose translated from docker commands:
    ```
    docker run myimage    ---> docker-compose up
    ```
    or:
    ```
    docker build.
                        ---> docker compose up --build
    docker run my image
    ```

- In the directory where the docker-compose file is located launch:
    ```
    docker-compose up -d
    ```
    and to stop the containers:
    ```
    docker-compose down
    ```

## Production workflow

- Using a development Dockerfile:
    ```
    docker build -f Dockerfile.dev
    ```

- Create reference to a local folder inside a container:
    ```
    docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app imageId
    ```
    Use ${PWD} which is correct for use with PowerShell

