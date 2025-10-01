# obs obs, since node (java) is not compiled, can't use multi-stage build to reduce image size!
FROM node:14-alpine AS build

WORKDIR /usr/src/app

COPY . .

RUN npm install

# production
RUN npm run build

FROM node:14-alpine AS runtime

WORKDIR /usr/src/app

COPY --from=build /usr/src/app/build ./build

RUN npm install -g serve

EXPOSE 5000

RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

CMD ["serve", "-s", "-l", "5000", "build"]
