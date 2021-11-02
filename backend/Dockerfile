# Pulling in the image containing java 16 development kit. Alpine is a slimline version of this.
FROM openjdk:16-alpine3.13

# Entering new directory in the container into which the files needed to run the springboot app will be copied
WORKDIR /app

# Copying the files needed to build and run the springboot app into the app directory. 
# 'check-db.sh' is a script that can test that the deployed app can communicate with the database on GCP.
COPY .mvn/ .mvn
COPY mvnw pom.xml ./
RUN ./mvnw dependency:go-offline
COPY src ./src

# These commands will be executed upon startup of the container, and initiate the springboot app.
CMD ["./mvnw", "spring-boot:run"]

# The backend app will be accessible over port 8080.
EXPOSE 8080

