FROM openjdk:11.0.16-jre-slim-buster

ARG PINPOINT_VERSION=${PINPOINT_VERSION:-2.5.1}
#ARG INSTALL_URL=https://github.com/pinpoint-apm/pinpoint/releases/download/v${PINPOINT_VERSION}/pinpoint-batch-${PINPOINT_VERSION}.jar

ARG INSTALL_URL=/root/pinpoint-docker-2.5.1/pinpoint-batch/build/pinpoint-batch-${PINPOINT_VERSION}.jar

RUN mkdir -p /pinpoint/config \
    && mkdir -p /pinpoint/scripts

COPY /build/config/pinpoint-batch.properties /pinpoint/config/
COPY /build/scripts/start-batch.sh /pinpoint/scripts/
COPY /build/pinpoint-batch-${PINPOINT_VERSION}.jar /pinpoint/pinpoint-batch.jar

RUN apt-get update && apt-get install --no-install-recommends -y curl && apt-get clean \
    && chmod a+x /pinpoint/scripts/start-batch.sh \
    && chmod a+x /pinpoint/config/pinpoint-batch.properties \

ENTRYPOINT ["sh", "/pinpoint/scripts/start-batch.sh"]