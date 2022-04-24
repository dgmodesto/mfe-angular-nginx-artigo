### STAGE 1:BUILD ###
FROM node:16.10-alpine AS build

WORKDIR /dist/src/app
RUN npm cache clean --force

COPY . .
RUN npm install
RUN npm run build --prod -- --deployUrl /advisor-module/

### STAGE 2:RUN ###
FROM nginx:latest AS ngi

COPY --from=build /dist/src/app/dist/mfe-advisor-module /usr/share/nginx/html
COPY ./config/nginx.conf /etc/nginx/nginx.conf

EXPOSE 80