FROM node:22 
# base image file get from hub.docker.com
# Which application we need and which version we want.

# make folder in the empty container
WORKDIR /myapp

# Copy our project file into containter
COPY . .

# install dependenciess
RUN npm install

# Optional by defaults node app run 3000
EXPOSE 3000 

# RUN npm start

CMD [ "npm", "start" ]


