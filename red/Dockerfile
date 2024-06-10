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
