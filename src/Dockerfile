FROM nginx:latest

RUN echo '<h1>sem conteudo<h1>' > /usr/share/nginx/html/conteudo.html
COPY *.html /usr/share/nginx/html/
FROM node:14.16.1-alpine3.13
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 8080
CMD ["node", "app.js"]
