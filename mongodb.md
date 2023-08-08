## MongoDB
### Command Line
```bash
docker run --name database -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password123 -p 27017:27017 -d mongo:latest
```
### Script
```
version: '3.8'
services:
  mongodb:
    image: mongo:latest
    container_name: my-mongodb
    restart: always
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: examplepassword
    volumes:
      - mongodb_data:/data/db

volumes:
  mongodb_data:
```