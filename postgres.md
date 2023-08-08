## PostgreSQL
### Command Line
```bash
docker run --name database -e POSTGRES_PASSWORD=password123 -p 5432:5432 -d postgres
```

### Script
```dockerfile
version: '3.8'
services:
  postgres:
    container_name: pgdatabase
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
    container_name: pgclient
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
