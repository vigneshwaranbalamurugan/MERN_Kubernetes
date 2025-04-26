# Frontend Dockerfile
FROM node:18-alpine as build

WORKDIR /app

# Copy package.json and package-lock.json first for better caching
COPY package*.json ./

RUN npm install

# Copy the rest of the frontend code
COPY . .

# Build the React app
RUN npm run build

# Production environment
FROM nginx:alpine

# Copy the build output to replace the default nginx contents
COPY --from=build /app/build /usr/share/nginx/html

# Copy custom nginx config to ensure React Router works properly
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose the specified frontend port
EXPOSE 3000

CMD ["nginx", "-g", "daemon off;"]