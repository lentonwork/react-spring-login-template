# Pulls in the Node image into the container, hereto referred to as 'build'. Alpine is a slimline version.
FROM node:12.4.0-alpine as build

# Entering a new directory in the container called app, in which to store all necessary code to run the application.
WORKDIR /app

# Copying a list of all the necessary dependencies the frontend app needs to import.
COPY package.json package-lock.json ./

# Installing all of those dependencies on the container.
RUN npm install
COPY . ./

# Creates an environment variable the frontend uses to access the backend when running locally. This is overwritten by the pipeline when pushing to GCP.
RUN echo "REACT_APP_API_BASE_URL=http://localhost:8080/" >> .env

# Building the application.
RUN npm run build

# The frontend app will be accessible on port 80. NOTE that this port is mapped to port 9090 by docker-compose.yaml, so when running locally using...
# docker compose, the frontend app should be found on port 9090.
EXPOSE 80

# These commands are run upon startup of the app - they initiate the web server. 'Daemon off' tells it to run in the foreground. 
ENTRYPOINT ["nginx","-g","daemon off;"]

