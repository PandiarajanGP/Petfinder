
FROM node:20-alpine AS build

WORKDIR /app


COPY package*.json ./
RUN npm i

RUN npm install -g @angular/cli


# Copy source code
COPY . .

# Build Angular app for production
RUN ng build 

# ===========================
# build optimize
# ===========================
FROM nginx:alpine

# Remove default NGINX website
RUN rm -rf /usr/share/nginx/html/*

# Copy built Angular app
COPY --from=build /app/dist/petmanagement /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf


# Expose port
EXPOSE 80

# Start NGINX
CMD ["nginx", "-g", "daemon off;"]

