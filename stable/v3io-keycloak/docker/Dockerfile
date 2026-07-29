ARG KEYCLOAK_IMAGE_VERSION=26.3.3-debian-12-r0

# if it fails to build and you see this comment,
# then make sure that buildx is enabled on your docker env or run with `DOCKER_BUILDKIT=1 make build`
FROM bitnamilegacy/keycloak:${KEYCLOAK_IMAGE_VERSION}

# mysql client is used by the heal-interrupted-migration init container (see
# stable/v3io-keycloak/values.yaml) to detect and recover from a first-time
# Liquibase migration that got interrupted before completion (IG-25046).
USER root
RUN install_packages default-mysql-client
USER 1001

ADD 0_startup_auth-path.sh /docker-entrypoint-initdb.d/0_startup_auth-path.sh
ADD libkeycloak.sh /opt/bitnami/scripts/libkeycloak.sh
