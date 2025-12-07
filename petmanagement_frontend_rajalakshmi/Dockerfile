
FROM node:20-alpine AS build

WORKDIR /app


COPY package*.json ./
RUN npm i

RUN npm install -g @angular/cli


COPY . .

RUN ng build 

FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/*

COPY --from=build /app/dist/petmanagement /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf


EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

