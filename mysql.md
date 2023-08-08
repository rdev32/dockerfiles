## MySQL
### Command Line
```bash
docker run --name database -e MYSQL_ROOT_PASSWORD=password123 -p 3306:3306 -d mysql
```

### Script
```dockerfile
version: '3.8'
services:
  mysql:
    image: mysql:latest
    container_name: mysql
    environment:
      MYSQL_ROOT_PASSWORD: your-root-password
      MYSQL_DATABASE: your-database
      MYSQL_USER: your-username
      MYSQL_PASSWORD: your-password
    ports:
      - "3306:3306"
```
