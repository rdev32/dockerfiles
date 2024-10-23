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

Create a folder named `/addons` in the same place where you put the `docker-compose.yml` file. All addons will be loaded directly into the instance.

```yaml
services:
  db:
    image: postgres:15
    container_name: data
    restart: always
    environment:
      POSTGRES_DB: odoo
      POSTGRES_USER: odoo
      POSTGRES_DB: postgres
      PGDATA: /var/lib/postgresql/data/pgdata

  odoo:
    image: odoo:17.0
    container_name: odoo
    ports:
      - "8069:8069"
    volumes:
      - ./config:/etc/odoo
      - ./addons:/mnt/extra-addons
    depends_on:
      - db
```

#### Settings

Create a file named `odoo.conf` inside a `/config` directory in the same place you put the `docker-compose.yml` with the following content.<br>
_Feel free to change any setting_ this will change the behaviour of your instance.

```
[options]
addons_path = /mnt/extra-addons
data_dir = /var/lib/odoo
; admin_passwd = admin
; csv_internal_sep = ,
; db_maxconn = 64
; db_name = False
; db_template = template1
; dbfilter = .*
; debug_mode = False
; email_from = False
; limit_memory_hard = 2684354560
; limit_memory_soft = 2147483648
; limit_request = 8192
; limit_time_cpu = 60
; limit_time_real = 120
; list_db = True
; log_db = False
; log_handler = [':INFO']
log_level = debug
; logfile = /var/log/odoo/odoo.log
; longpolling_port = 8072
; max_cron_threads = 2
; osv_memory_age_limit = 1.0
; osv_memory_count_limit = False
; smtp_password = False
; smtp_port = 25
; smtp_server = localhost
; smtp_ssl = False
; smtp_user = False
; workers = 0
; xmlrpc = True
; xmlrpc_interface =
; xmlrpc_port = 8069
; xmlrpcs = True
; xmlrpcs_interface =
; xmlrpcs_port = 8071
```
