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
FROM openjdk:17

EXPOSE 8080

ADD target/buyLeaf-0.0.1-SNAPSHOT.jar app.jar

ENTRYPOINT ["java","-jar","/app.jar"]
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