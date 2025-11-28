# Multi-stage Dockerfile for building and serving the Angular frontend

# --- Build stage ---
FROM node:18-alpine AS build
WORKDIR /app

# install dependencies (use package-lock when present)
COPY package*.json ./
RUN npm ci --silent

# copy sources and build
COPY . .
RUN npm run build -- --configuration production

# --- Production stage ---
FROM nginx:stable-alpine

# Copy built app from build stage
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

# Replace default nginx config with one suited for SPA routing
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
