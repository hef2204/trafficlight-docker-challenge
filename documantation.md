1. Clone the Repository
First, clone the repository to your local machine:

```bash
git clone https://github.com/hayk96/trafficlight-docker-challenge
cd trafficlight-docker-challenge

2. Create Dockerfile for Each Application
Create a Dockerfile in each application directory (red, yellow, green). Here is the example Dockerfile:

# Use the specified base image
FROM node:17.0-alpine3.14

# Set the working directory
WORKDIR /app

# Copy package files before installation
COPY package*.json ./

# Install npm with the specified version using apk
RUN apk add --no-cache npm=7.17.0-r0

# Install dependencies
RUN npm install

# Copy the application code
COPY . .

# Create the views directory
RUN mkdir -p /app/views

# Copy specific files to the /app/views directory
COPY index.pug /app/views/
COPY favicon.ico /app/views/

# Expose the necessary port
EXPOSE 80

# Command to run the application
CMD ["node", "app.js"]

3. Build Docker Images

3. Build Docker Images
Navigate to each application directory and build the Docker images:

Build for Red Application:


cd red
docker build -t trafficlight/red:v1.0 .
cd ..
Build for Yellow Application:


cd yellow
docker build -t trafficlight/yellow:v1.0 .
cd ..
Build for Green Application:


cd green
docker build -t trafficlight/green:v1.0 .
cd ..

4. Create a Docker Network
Create a custom Docker network for the applications to communicate:

docker network create --subnet=172.20.0.0/16 --gateway=172.20.0.1 traffic-light

5. Stop and Remove Existing Containers (if any)
Stop and remove any existing containers to avoid conflicts:

docker stop red-app yellow-app green-app nginx-proxy
docker rm red-app yellow-app green-app nginx-proxy

6. Run Docker Containers for Each Application
Execute the following commands to run each container and assign them to the created network:

Run Red Application Container:
docker run -d --name red-app --net traffic-light trafficlight/red:v1.0

Run Yellow Application Container:

docker run -d --name yellow-app --net traffic-light trafficlight/yellow:v1.0

Run Green Application Container:

docker run -d --name green-app --net traffic-light trafficlight/green:v1.0

7. Pull and Run the Nginx Container:

docker pull nginx:1.21
docker run -d --name nginx-proxy --net traffic-light -v ~/nginx/conf.d/:/etc/nginx/conf.d/ nginx:1.21

8. Verify Running Containers:

docker ps -a 


2. Create Dockerfile for Each Application
Create a Dockerfile in each application directory (red, yellow, green). Here is the sample Dockerfile:

# Use the specified base image
FROM node:17.0-alpine3.14

# Set the working directory
WORKDIR /app

# Copy package files before installation
COPY package*.json ./

# Install npm with the specified version using apk
RUN apk add --no-cache npm=7.17.0-r0

# Install dependencies
RUN npm install

# Copy the application code
COPY . .

# Create the views directory
RUN mkdir -p /app/views

# Copy specific files to the /app/views directory
COPY index.pug /app/views/
COPY favicon.ico /app/views/

# Expose the necessary port
EXPOSE 80

# Command to run the application
CMD ["node", "app.js"]

3. Build Docker Images

3. Build Docker Images
Navigate to each application directory and build the Docker images:

Build for Red Application:


cd red
docker build -t trafficlight/red:v1.0 .
cd ..
Build for Yellow Application:


cd yellow
docker build -t trafficlight/yellow:v1.0 .
cd ..
Build for Green Application:


cd green
docker build -t trafficlight/green:v1.0 .
cd ..

4. Create a Docker Network
Create a custom Docker network for the applications to communicate:

docker network create --subnet=172.20.0.0/16 --gateway=172.20.0.1 traffic-light

5. Stop and Remove Existing Containers (if any)
Stop and remove any existing containers to avoid conflicts:

docker stop red-app yellow-app green-app nginx-proxy
docker rm red-app yellow-app green-app nginx-proxy

6. Run Docker Containers for Each Application
Execute the following commands to run each container and assign them to the created network:

Run Red Application Container:
docker run -d --name red-app --net traffic-light trafficlight/red:v1.0

Run Yellow Application Container:

docker run -d --name yellow-app --net traffic-light trafficlight/yellow:v1.0

Run Green Application Container:

docker run -d --name green-app --net traffic-light trafficlight/green:v1.0

7. Pull and Run the Nginx Container:

docker pull nginx:1.21
docker run -d --name nginx-proxy --net traffic-light -v ~/nginx/conf.d/:/etc/nginx/conf.d/ nginx:1.21

8. Verify Running Containers:

docker ps -a 
