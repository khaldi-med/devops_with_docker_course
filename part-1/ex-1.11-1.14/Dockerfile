# From docker Hub running Java provided by amazonecorretto
FROM amazoncorretto:8

EXPOSE 8080

WORKDIR /usr/src/app

# Copy the files required for dependencies to be installed
COPY mvnw* ./

# Copy all of the source code
COPY . .

RUN ./mvnw package

# The command to run the application
CMD ["java", "-jar", "./target/docker-example-1.1.3.jar"]
