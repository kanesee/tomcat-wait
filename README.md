# tomcat-wait
Docker build for a tomcat service that waits for containers to be ready before starting

Often times, your tomcat webapp needs a database connection to be available on startup. With this image, you can do that by simply adding a WAIT_HOSTS environment variable to docker-compose.yml

```
version: '3'
services:
  mysql:
    image: "mysql:5.7"
    container_name: mysql
    ports:
      - "3306:3306"
  my_app:
    image: "kanesee/tomcat-wait"
    environment:
      WAIT_HOSTS: mysql:3306
```

This image was built off the [official tomcat Dockerfile](https://hub.docker.com/_/tomcat/) and incorporates [ufoscout/docker-compose-wait](https://github.com/ufoscout/docker-compose-wait).
