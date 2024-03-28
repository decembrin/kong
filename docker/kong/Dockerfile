FROM node:20.6-alpine as builder

RUN apk add git

WORKDIR /usr/src/app

COPY ./kong-manager/package*.json ./
RUN yarn install

COPY ./kong-manager/ ./
RUN yarn build

FROM kong:3.4-ubuntu

USER root

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        netcat \
    && rm -rf /var/lib/apt/lists/*

COPY ./docker/kong/entrypoint.sh /usr/local/bin/
RUN chmod 755 /usr/local/bin/entrypoint.sh

USER kong

COPY --from=builder /usr/src/app/dist /usr/local/kong-manager

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]

CMD ["kong", "docker-start"]
