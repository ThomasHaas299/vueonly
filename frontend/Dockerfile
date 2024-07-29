FROM node:iron-alpine3.20 AS base
WORKDIR /app

#dev stage
FROM base AS development-stage
#COPY package*.json ./
#RUN npm install
#COPY . .
EXPOSE 80
CMD ["npm", "run", "dev"]

# build stage
FROM base AS build-stage
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# test stage
FROM build-stage AS test-stage
RUN npm run test

# production stage
FROM nginx:stable-alpine AS production-stage
COPY --from=test-stage /app/dist /usr/share/nginx/html
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]