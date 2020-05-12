a./

configuration Dockerfile :

# Create image based on the official Node 6 image from the dockerhub
FROM node:6

# Create a directory where our app will be placed
RUN mkdir -p /usr/src/app

# Change directory so that our commands run inside this new directory
WORKDIR /usr/src/app

# Copy dependency definitions
COPY package*.json /usr/src/app/

# Install dependecies
RUN npm install

# Get all the code needed to run the app
COPY . /usr/src/app/

# Expose the port the app runs in
EXPOSE 8080

# Serve the app
CMD ["npm", "start"]

b.docker-compose 

#définir la version 

version: "2"
#définir les service

services:
    frontend:
        build: frontend
        
        #définir les ports

        ports:
            - "3000:3000"

    backend:
        build: backend
        ports:
            - "8080:8080"

    mongodb:
        image: mongo
        restart: always
        container_name: mongodb
        volumes:
            - ./data-node:/data/db
        ports:
            - 27017:27017
        command: mongod --noauth