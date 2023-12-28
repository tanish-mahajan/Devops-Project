# Website Architecture

  * Index.html: Frontend
  * Node: Backend
  * MongoDB: Database
  * MongoExpress: Mongo UI

# Docker Commands
  ### Initial Commands:
    docker network create mongo-network
    docker pull mongo
    docker pull mongo-express
  ### MongoDB:
    docker run -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --network mongo-network -d mongo
  ### MongoExpress:
    docker run -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password -e ME_CONFIG_MONGODB_SERVER=mongodb -d --network mongo-network --name mongo-express mongo-express
  * login with admin:pass in mongoexpress
  * Create database user-accounts

# Docker Compose YAML File
    version: '3.8'
    services:
      mongodb:
        image: mongo
        ports:
          - 27017:27017
        environment:
          - MONGO_INITDB_ROOT_USERNAME=admin
          - MONGO_INITDB_ROOT_PASSWORD=password
    
      mongo-express:
        image: mongo-express
        ports:
          - 8081:8081
        environment:
          - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
          - ME_CONFIG_MONGODB_ADMINPASSWORD=password
          - ME_CONFIG_MONGODB_SERVER=mongodb
 ### Run with command
    docker-compose -f docker-compose.yaml up -d
 ### Stop all containers
    docker-compose -f docker-compose.yaml down
 

