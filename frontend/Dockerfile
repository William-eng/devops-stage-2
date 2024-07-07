# Stage 1: Build the React app
FROM node:18 AS build

ARG VITE_API_URL=http://localhost:8000

ENV VITE_API_URL=$VITE_API_URL
WORKDIR /app
COPY package*.json .
RUN npm install
COPY . .

RUN npm install -g typescript
RUN npm run build
RUN echo "Build output:" && npm run build
RUN echo "Contents of /app:" && ls -la /app

# Check the contents of the build directory
RUN echo "Contents of /app/build:" && ls -la /app/dist

# Stage 2: Serve the React app with Nginx
FROM nginx:alpine

# Copy the built React app from the previous stage to the nginx web root
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start the nginx server
CMD ["nginx", "-g", "daemon off;"]
