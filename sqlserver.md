## Microsoft SQLServer Docker Setup [\*](https://hub.docker.com/r/microsoft/mssql-server)

This Docker configuration sets up an instance of Microsoft SQL Server, a relational database management system. It includes a command-line example for quick deployment and a `docker-compose` script for managing the service in a project.

| **Argument**  | **Description**                                                   |
| ------------- | ----------------------------------------------------------------- |
| `ACCEPT_EULA` | Required to accept Microsoft's End-User License Agreement (EULA). |
| `SA_PASSWORD` | Sets the password for the system administrator (SA) account.      |

### Docker command

```bash
docker run --name mssql-tests -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=Password123" -e "MSSQL_PID=Express" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

### Docker compose

```yaml
services:
  sqlserver:
    image: mcr.microsoft.com/mssql/server:2019-latest
    container_name: my-sqlserver
    restart: always
    ports:
      - '1433:1433'
    environment:
      MSSQL_PID: Express
      MSSQL_SA_PASSWORD: Password123
      ACCEPT_EULA: Y

volumes:
  sqlserver_data:
```
