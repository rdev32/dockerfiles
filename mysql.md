## MySQL Docker Setup [\*](https://hub.docker.com/_/mysql)

This Docker configuration sets up a MySQL database instance. It includes a command-line example for quick deployment and a `docker-compose` script for managing the service in a project.

| **Argument**          | **Description**                                      |
| --------------------- | ---------------------------------------------------- |
| `MYSQL_ROOT_PASSWORD` | Sets the root user password.                         |
| `MYSQL_DATABASE`      | Creates a default database.                          |
| `MYSQL_USER`          | Creates a non-root user with access to the database. |
| `MYSQL_PASSWORD`      | Sets the password for the non-root user.             |

### Docker command

```bash
docker run --name database \
  -e MYSQL_ROOT_PASSWORD=password \
  -p 3306:3306 \
  -d mysql
```

### Docker compose

```yaml
services:
  mysql:
    image: mysql:latest
    container_name: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root-password
      MYSQL_DATABASE: database
      MYSQL_USER: username
      MYSQL_PASSWORD: password
    ports:
      - '3306:3306'
```
