# Stage 1: Build React app
FROM node:20-alpine AS build

WORKDIR /usr/src/app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install --legacy-peer-deps

# Copy the rest of the app and build
COPY . .
RUN npm run build

# Stage 2: Serve with NGINX
FROM nginx:1.25.2-alpine

# Copy build output from previous stage to nginx html folder
COPY --from=build /usr/src/app/dist /usr/share/nginx/html

# Copy custom nginx config if needed
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]


