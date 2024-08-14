## MongoDB Docker Setup [\*](https://hub.docker.com/_/mongo)

This Docker configuration sets up an instance of MongoDB, a popular NoSQL database, with user-defined credentials. It also provides a `docker-compose` script to manage the service in a project setup.

| **Parameter**                | **Explanation**                        |
| ---------------------------- | -------------------------------------- |
| `MONGO_INITDB_ROOT_USERNAME` | The username for the MongoDB root user |
| `MONGO_INITDB_ROOT_PASSWORD` | The password for the MongoDB root user |

### Docker command

```bash
docker run --name mongodb-instance \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=password123 \
  -p 27017:27017 \
  -d mongo:latest
```

### Docker compose

```yaml
services:
  mongodb:
    image: mongo:latest
    container_name: mongodb
    restart: always
    ports:
      - '27017:27017'
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: password
    volumes:
      - mongodb_data:/data/db

volumes:
  mongodb_data:
```
