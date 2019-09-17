FROM alpine:latest AS builder

ARG MVN_REPO=https://repo1.maven.org/maven2
ARG VERSION=3.1.0

WORKDIR /hygieia

RUN apk add --no-cache wget \
    && wget --no-check-certificate -q ${MVN_REPO}/com/capitalone/dashboard/UI/${VERSION}/UI-${VERSION}-src.tar.gz \
    && wget --no-check-certificate -q ${MVN_REPO}/com/capitalone/dashboard/UI/${VERSION}/UI-${VERSION}-src.tar.gz.sha1 \
    && echo "Verifying checksum" \
    && echo "$(cat UI-${VERSION}-src.tar.gz.sha1)  UI-${VERSION}-src.tar.gz" | sha1sum -c - \
    && tar xvf UI-${VERSION}-src.tar.gz --strip 1

FROM nginx:alpine

COPY --from=builder /hygieia/dist/ /usr/share/nginx/html/
