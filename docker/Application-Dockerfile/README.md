# Different Applications Dockerfiles


## Python 
```Dockerfile
# The first instruction is what image we want to base our container on
# We Use an official Python runtime as a parent image
FROM python:3.10

# The enviroment variable ensures that the python output is set straight
# to the terminal with out buffering it first
ENV PYTHONUNBUFFERED 1

# create root directory for our project in the container
RUN mkdir /app

# Set the working directory to /music_service
WORKDIR /app

COPY . .

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt
```

## Java (maven)
```Dockerfile
FROM maven:3.8.4-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean install

FROM openjdk:17-jre-slim

# Set the working directory to /app
WORKDIR /app
# Copy the generated SNAPSHOT jar from build to /app
COPY --from=build /app/target/<APP>.jar app.jar

# Make port 8080 available to the world outside this container
EXPOSE 8080

# Run the JAR file when the container launches
CMD ["java", "-jar", "app.jar"]
```

## Node js (npm)

```Dockerfile
FROM node:20

WORKDIR /app
COPY package*.json ./
RUN npm install && npm prune --production

COPY . .
EXPOSE 8000
CMD ["node", "index.js"]
```