## PostgreSQL Docker Setup [\*](https://hub.docker.com/_/postgres)

This Docker configuration sets up a PostgreSQL database along with PgAdmin, a web-based database management tool. The setup includes both a command-line example for quick deployment and a `docker-compose` script for managing the services in a project.

| **Argument**               | **Description**                                                  |
| -------------------------- | ---------------------------------------------------------------- |
| `POSTGRES_PASSWORD`        | Sets the password for the default `postgres` user.               |
| `POSTGRES_USER`            | Specifies the PostgreSQL user that owns the database (optional). |
| `POSTGRES_DB`              | Creates a default database (optional).                           |
| `PGADMIN_DEFAULT_EMAIL`    | Sets the default email for PgAdmin login.                        |
| `PGADMIN_DEFAULT_PASSWORD` | Sets the default password for PgAdmin login.                     |

### Docker command

```bash
docker run --name database \
  -e POSTGRES_PASSWORD=password123 \
  -p 5432:5432 \
  -d postgres
```

### Docker compose

```yaml
services:
  postgres:
    container_name: database
    image: postgres
    restart: always
    ports:
      - '5432:5432'
    environment:
      DATABASE_HOST: 127.0.0.1
      POSTGRES_USER: root
      POSTGRES_PASSWORD: root
      POSTGRES_DB: mydb

  pgadmin:
    container_name: client
    image: dpage/pgadmin4
    restart: always
    environment:
      PGADMIN_DEFAULT_EMAIL: 'admin@admin.com'
      PGADMIN_DEFAULT_PASSWORD: 'admin'
    ports:
      - '9090:80'
    depends_on:
      - postgres
```
