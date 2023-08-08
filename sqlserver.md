## SQLServer
### Command Line
```bash
docker run --name database -e ACCEPT_EULA=Y -e SA_PASSWORD=password123 -p 1433:1433 -d mcr.microsoft.com/mssql/server:latest
```

### Script
```dockerfile
version: '3.8'
services:
  sqlserver:
    image: mcr.microsoft.com/mssql/server:2019-latest
    container_name: my-sqlserver
    restart: always
    ports:
      - "1433:1433"
    environment:
      SA_PASSWORD: password123
      ACCEPT_EULA: Y

volumes:
  sqlserver_data:
```