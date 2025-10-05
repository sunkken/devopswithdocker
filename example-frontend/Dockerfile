# obs obs, since node (java) is not compiled, 
# multi-stage build with prod starting from node doesn't help much.
FROM node:14-alpine AS build-stage

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm ci

COPY . .

RUN npm run build

# production
FROM nginx:1.25-alpine

WORKDIR /usr/src/app

COPY --from=build-stage /usr/src/app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
