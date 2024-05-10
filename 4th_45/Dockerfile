FROM node:14
# Base Image and Version

WORKDIR /app
# Working Directory inside of Docker Container

COPY package.json /app
# Copy dependencies to Working Directory

RUN npm install
# Install all dependencies mentioned in package.json

COPY . .
# Copy remaining code to Working Directory
# Container and Image have own "Isolated" file system 
# Copy local folder to Docker => No connection or reflection between Local and Docker

EXPOSE 80
# Expose port 

VOLUME [ "/app/feedback" ]
# Inside of Container should be mapped to Ouside of Container 

CMD [ "node", "server.js" ]
# Specify command want to execute when container started based on this image

# Start this dockerfile 
# 1. docker build -t feedback-node 
#     => Create Docker Image (default tag => :latest)
# 2. docker run -p 3000:80 -d --name feedback-app --rm feedback-node:latest 
#     => Start Docker Container based on this Docker Image
#     => -p : Expose port (local : 3000, docker : 80)
#     => -d : detached mode 
#     => --name : name the Container 
#     => --rm : automatically remove container when stop 