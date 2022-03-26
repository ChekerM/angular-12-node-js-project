### STAGE 1: Build ###
FROM node:16-alpine3.12 AS build 
WORKDIR /usr/src/app
COPY package.json ./
RUN npm install --force
COPY . .
ARG configuration=production
RUN npm run build -- --outputPath=./dist/out --configuration $configuration
#RUN npm run build --prod

### STAGE 2: Run ###
FROM nginx:alpine
COPY --from=build /usr/src/app/dist/out/ /usr/share/nginx/html
#COPY /nginx-custom.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
ENTRYPOINT ["nginx","-g","daemon off;"]
