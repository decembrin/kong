FROM node:20.6-alpine as builder

RUN apk add git

WORKDIR /usr/src/app

COPY ./kong-manager/package*.json ./

RUN yarn install

COPY ./kong-manager/ ./

RUN yarn build

FROM bitnami/openresty:1.21-debian-11

COPY --from=builder /usr/src/app/dist /app
