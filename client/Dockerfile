# Production environment

# Phase 1 - temporary container to build our React app
FROM node:alpine as builder
WORKDIR /app
COPY ./package.json ./
RUN npm install
COPY ./ ./
RUN npm run build

# Phase 2 - the final container will contain only the build folder with our built React app
# nginx is web server we use to host our static React app content
FROM nginx

# The port our react app uses
EXPOSE $PORT

# put our built React app in the nginx folder for hosting static content 
# builder comes from Phase 1
COPY --from=builder /app/build /usr/share/nginx/html

# override nginx configuration with our own
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf


