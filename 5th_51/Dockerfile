FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install
# "RUN npm install" => Installing and making dependencies folder inside of Docker Container

COPY . .
# Copy all Local file to Inside of Docker Container WORKDIR "/app"

# Local file may override this dependencies file and making error 

### Need to managing Local file to copy and inside of Docker Container 
# 1. Volume
# 2. Bind Mounts
# 3. .dockerignore 

ARG DEFAULT_PORT=80
### Buildtime ARGuments 
# only use in Dockerfile, not in code or file 
# can make Dockerfile dynamic by using ARG
# => can make various image from same Dockerfile 

# not a fixed value, can configure while Docker Image build 
# => docker build ~~ --build-arg DEFAULT_PORT=80 ~~

ENV PORT1 $DEFAULT_PORT \
    PORT2=200
# ENV PORT 80

### Runtime ENVironment Variable
# Created by ARG in Dockerfile to make variable dynamic
# Specify by $ in front of ARG name to notify Docker 

# not a fixed value, can configure while Docker Container run 
# => docker run ~~ --env PORT1=199 -e PORT2=200 ~~ 

EXPOSE $PORT
# Using ENVIronment Variable 
# -> Instance of using ENV varibale, can make various Image from same Container
# Specify by $ in front of ENV name to notify Docker 

# VOLUME [ "/app/node_modules" ]
# To make 1.1 Anonymous Volume
# Can make in both Dockerfile or CLI when executing Docker Container 

CMD [ "npm", "start" ]

# when executing Docker Container CLI, making Volume or Bind_Mounts 

# docker run ~~ 
#       -v feedback:/app/feedback                                       => 1-2. Named_Volume
#       -v ""Local absolute Path":"Mounting Path inside Container":ro"  => 2. Bind_Mounts (Read-Only Mode)
#       -v /app/node_modules                                            => 1-1. Anonymous_Volume
#       -v /app/temp                                                    => 1-1. Anonymous_Volume
# ~~