# Website

  * Index.html: Frontend
  * Node: Backend
  * MongoDB: Database
  * MongoExpress: Mongo UI

# Docker Commands
  ### Important Commands
    docker network create mongo-network
  ### MongoDB:
    docker pull mongo
    docker run -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --network mongo-network -d mongo
  ### MongoExpress:
    docker pull mongo-express
    docker run -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password -e ME_CONFIG_MONGODB_SERVER=mongodb -d --network mongo-network --name mongo-express mongo-express
  ***login with admin:pass in mongoexpress***
