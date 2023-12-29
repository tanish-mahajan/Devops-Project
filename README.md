# Website Architecture

  * Index.html: Frontend
  * Node: Backend
  * MongoDB: Database
  * MongoExpress: Mongo UI
# Build Docker Image for Application
    FROM node:13-alpine
    
    RUN mkdir -p /home/app
    
    COPY ./app /home/app
    
    # set default dir so that next commands executes in /home/app dir
    WORKDIR /home/app
    
    # will execute npm install in /home/app because of WORKDIR
    RUN npm install
    
    # no need for /home/app/server.js because of WORKDIR
    CMD ["node", "server.js"]
    
### Docker commands for Application Image:
    docker build -t my-app:1.0 .

# Docker Commands for MongoDB and MongoExpress
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
      my-app:
        image: my-app:1.0
        ports:
          - 3000:3000
          
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
 ### Run all containers
    docker-compose -f docker-compose.yaml up -d
 ### Stop all containers
    docker-compose -f docker-compose.yaml down
 

