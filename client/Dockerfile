#build phase
FROM node:16-alpine as builder
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
RUN npm run build
# after this there will be a folder /app/build

#run phase
FROM nginx
# need to expose port for deployment
EXPOSE 3000
# copy from the builder phase. The destination folder is a setting from nginx
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build  /usr/share/nginx/html