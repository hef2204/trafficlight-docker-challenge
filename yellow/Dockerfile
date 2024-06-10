
FROM node:17.0-alpine3.14
WORKDIR /app
COPY package*.json ./
RUN apk add --no-cache npm=7.17.0-r0
RUN npm install
COPY . .
RUN mkdir -p /app/views
COPY index.pug /app/views/
COPY favicon.ico /app/views/
EXPOSE 80

CMD ["node", "app.js"]
