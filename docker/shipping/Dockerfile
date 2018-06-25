FROM weaveworksdemos/msd-java:jre-latest

RUN apk add --update gcc musl-dev linux-headers

WORKDIR /usr/src/app
COPY *.jar ./app.jar

RUN	chown -R ${SERVICE_USER}:${SERVICE_GROUP} ./app.jar

COPY rbinder.c rbinder.c
COPY uthash.h uthash.h
RUN gcc -o rbinder rbinder.c

USER ${SERVICE_USER}

#ARG BUILD_DATE
#ARG BUILD_VERSION
#ARG COMMIT
#
#LABEL org.label-schema.vendor="Weaveworks" \
#  org.label-schema.build-date="${BUILD_DATE}" \
#  org.label-schema.version="${BUILD_VERSION}" \
#  org.label-schema.name="Socks Shop: Shipping" \
#  org.label-schema.description="REST API for Shipping service" \
#  org.label-schema.url="https://github.com/microservices-demo/shipping" \
#  org.label-schema.vcs-url="github.com:microservices-demo/shipping.git" \
#  org.label-schema.vcs-ref="${COMMIT}" \
#  org.label-schema.schema-version="1.0"

ENTRYPOINT ["/usr/src/app/rbinder", "/usr/local/bin/java.sh","-jar","/usr/src/app/app.jar", "--port=8080"]
#ENTRYPOINT ["/usr/local/bin/java.sh","-jar","/usr/src/app/app.jar", "--port=8080"]
