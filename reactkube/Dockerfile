# Stage 0, "build-stage", based on Node.js, to build and compile the frontend
FROM node:10.8.0 as build-stage
WORKDIR /app
COPY package*.json /app/
RUN npm install
COPY ./ /app/
ARG configuration=uat
EXPOSE 80
RUN npm run build --configuration $configuration

# Stage 1, based on Nginx, to have only the compiled app, ready for production with Nginx
FROM nginx:1.15
#Copy ci-dashboard-dist
COPY --from=build-stage /app/dist/lfa/ /usr/share/nginx/html
#Copy default nginx configuration
COPY ./nginx/nginx-custom.conf /etc/nginx/conf.d/default.conf