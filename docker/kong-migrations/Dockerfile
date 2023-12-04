FROM kong/kong-gateway:3.4-debian

USER root

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        netcat \
    && rm -rf /var/lib/apt/lists/*

COPY ./docker/kong-migrations/entrypoint.sh /usr/local/bin/
RUN chmod 755 /usr/local/bin/entrypoint.sh

USER kong
