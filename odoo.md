## Odoo 17 Community Docker Setup [\*](https://hub.docker.com/_/odoo)

This Docker configuration sets up an instance of Odoo 17 Community, an open-source ERP and CRM platform. It also includes a PostgreSQL database as the backend for storing all Odoo data. This setup provides a ready-to-use development or testing environment for Odoo.

| **Parameter**       | **Explanation**                                           |
| ------------------- | --------------------------------------------------------- |
| `POSTGRES_DB`       | The name of the PostgreSQL database for Odoo.             |
| `POSTGRES_USER`     | The PostgreSQL user for accessing the database.           |
| `POSTGRES_PASSWORD` | The password for the PostgreSQL user.                     |
| `ODOO_DB_HOST`      | The hostname of the PostgreSQL database (set to `db`).    |
| `ODOO_DB_USER`      | The Odoo database user (same as PostgreSQL user).         |
| `ODOO_DB_PASSWORD`  | The Odoo database password (same as PostgreSQL password). |

### Docker command

```bash
docker run --name odoo-db \
  -e POSTGRES_DB=odoo \
  -e POSTGRES_USER=odoo \
  -e POSTGRES_PASSWORD=odoo123 \
  -d postgres:13

docker run --name odoo \
  -p 8069:8069 \
  --link odoo-db:db \
  -e ODOO_DB_HOST=db \
  -e ODOO_DB_USER=odoo \
  -e ODOO_DB_PASSWORD=odoo123 \
  -d odoo:17.0
```

### Docker compose

```yaml
services:
  db:
    image: postgres:13
    container_name: odoo-db
    restart: always
    environment:
      POSTGRES_DB: odoo
      POSTGRES_USER: odoo
      POSTGRES_PASSWORD: odoo123
    volumes:
      - odoo-db-data:/var/lib/postgresql/data
    networks:
      - odoo-network

  odoo:
    image: odoo:17.0
    container_name: odoo
    depends_on:
      - db
    ports:
      - '8069:8069'
    environment:
      ODOO_DB_HOST: db
      ODOO_DB_USER: odoo
      ODOO_DB_PASSWORD: odoo123
    volumes:
      - odoo-data:/var/lib/odoo
    networks:
      - odoo-network

volumes:
  odoo-db-data:
  odoo-data:

networks:
  odoo-network:
```
