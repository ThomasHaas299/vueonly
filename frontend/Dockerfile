FROM node:iron-alpine3.20 as base
WORKDIR /app

#dev stage
FROM base as development-stage
#COPY package*.json ./
#RUN npm install
#COPY . .
EXPOSE 80
CMD ["npm", "run", "dev"]

# build stage
FROM base as build-stage
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# production stage
FROM nginx:stable-alpine as production-stage
COPY --from=build-stage /app/dist /usr/share/nginx/html
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]