# Stage 1: Build React static bundle
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package descriptors and install dependencies
COPY package*.json ./
RUN npm ci --quiet || npm install --quiet

# Copy source files and execute build
COPY . .
RUN npm run build

# Stage 2: Serve React application with Nginx
FROM nginx:alpine

# Remove default Nginx static assets
RUN rm -rf /usr/share/nginx/html/*

# Copy built web artifacts from builder stage
COPY --from=builder /app/build /usr/share/nginx/html

# Expose HTTP port 80
EXPOSE 80

# Run Nginx in foreground
CMD ["nginx", "-g", "daemon off;"]
