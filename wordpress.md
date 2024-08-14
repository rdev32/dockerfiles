# Wordpress Site

Creates a Wordpress instance with MySQL and PhpMyAdmin

## Script

```
services:
  db:
    container_name: db
    image: mysql:5.7
    volumes:
      - db:/var/lib/mysql
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=password
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=wordpress
    networks:
      - wpsite
  phpmyadmin:
    depends_on:
      - db
    image: phpmyadmin/phpmyadmin
    restart: always
    ports:
      - '8080:80'
    environment:
      - PMA_HOST=db
      - MYSQL_ROOT_PASSWORD=password
    networks:
      - wpsite
  wordpress:
    container_name: wp
    depends_on:
      - db
    image: wordpress
    ports:
      - '8000:80'
    restart: always
    volumes:
      - wordpress:/var/www/html
    environment:
      - WORDPRESS_DB_HOST=db:3306
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=wordpress
    networks:
      - wpsite
networks:
  wpsite:
volumes:
  db:
  wordpress:
```
