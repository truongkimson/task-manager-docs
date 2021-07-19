# Getting started

## Pre-requisite

In order to build and deploy the application locally, you'll need the following dependencies:

1. Docker - [link](https://www.docker.com/products/docker-desktop)
2. Git - [link](https://git-scm.com/downloads)

## Build Docker images

1. Clone the `fullstack-task-manager` to your local machine from [here](https://github.com/truongkimson/fullstack-task-manager)

2. Navigate to `task-manager` directory

    ```bash
    cd task-manager
    ```

3. Build Docker image for back-end Dropwizard service using

    ```bash
    docker build -t <docker-image-name>:<version-tag> .
    ```

4. Navigate to `task-manager-client/src/api/TaskAPI.js` and ensure the `HOST` value is set to `'http://localhost:8080'`

5. Build Docker image for ReactJs client using

    ```bash
    docker build -t <docker-image-name>:<version-tag> .
    ```

6. Pull official Docker image for MySQL 8.0

    ```bash
    docker pull mysql:8.0
    ```

7. Check that you have all three Docker images `<backend service image>`, `<client image>` and `mysql:8.0`

    ```bash
    docker image ls
    ```

## Deploy locally with `docker-compose`

1. Navigate back to root directory `fullstack-task-manage`
   
2. Open up `docker-compose.yml` file

    ```yml
    version: "3.9"
    services:
        db:
            image: mysql:8.0
            environment:
                - MYSQL_ROOT_PASSWORD=password
                - MYSQL_DATABASE=task-db
                - MYSQL_USER=task-service
                - MYSQL_PASSWORD=password
            volumes:
                - db-data:/var/lib/mysql
            container_name: mysql1
        web:
            image: syd.ocir.io/sdvw2vh5qake/task-manager/service:1.0
            ports:
                - "8080:8080"
            restart: always
            links:
                - db
            depends_on:
                - "db"
            container_name: task-service
        client:
            image: syd.ocir.io/sdvw2vh5qake/task-manager/client:1.0
            ports:
                - "80:80"
            restart: always
            depends_on:
                - "web"
            container_name: task-client
    volumes:
        db-data:
    ```

    Ensure the following values match the names given to your Docker images

    ```yml
     web:
         image: <your-service-image-name>:<version-tag>
     client:
         image: <your-client-image-name>:<version-tag>
    ```

3. Run the following command to deploy Docker containers

    ```bash
    docker-compose up -d
    ```

4. Wait till the deployment is finished. You should be able to see 3 containers running 

    ```bash
    docker ps
    ```

    ```
    CONTAINER ID   IMAGE                     COMMAND                  CREATED        STATUS        PORTS                    NAMES
    028980e2a15c   task-manager-client:1.0   "/docker-entrypoint.…"   16 hours ago   Up 16 hours   0.0.0.0:80->80/tcp       task-client
    7f6441710999   task-manager:1.0          "bash ./startup.sh"      16 hours ago   Up 16 hours   0.0.0.0:8080->8080/tcp   task-service
    08bf55498a2a   mysql:8.0                 "docker-entrypoint.s…"   16 hours ago   Up 16 hours   3306/tcp, 33060/tcp      mysql1
    ```

5. Visit `http://localhost/` to verify that the application is running correctly

## Deploy on remote host

In order deploy the application remotely, you can create a secure connection into the remote host and repeat the steps above, or you can create a `remote` context using `docker context` and deploy from your local machine.

More instructions on how to deploy to remote host using `docker context` can be found [here](https://www.docker.com/blog/how-to-deploy-on-remote-docker-hosts-with-docker-compose/)