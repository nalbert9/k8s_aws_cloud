# Pull official base image
FROM node:19-alpine as builder

WORKDIR /app

# Copy app files
COPY . .

# Install dependencies
RUN npm ci
# Build the app
RUN npm run build

# Bundle static assets with nginx
FROM nginx:1.23.2-alpine as production
ENV NODE_ENV production

# Copy built assets from `builder` image
COPY --from=builder /app/build /usr/share/nginx/html

# Add the nginx.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]