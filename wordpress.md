# [WordPress](https://hub.docker.com/_/wordpress)

This Docker Compose configuration sets up a complete WordPress environment with three services: WordPress, MySQL, and PhpMyAdmin.

- **MySQL** serves as the database for WordPress, storing all the site’s data.
- **PhpMyAdmin** provides an easy-to-use web interface to manage the MySQL database.
- **WordPress** is the content management system (CMS) that powers your website, ready to run on a customizable local server.

This setup allows for easy deployment and management of a WordPress site with persistent data storage and a user-friendly database management interface.

## Docker compose

```yaml
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
