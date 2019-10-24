FROM openjdk:alpine

# Input the setup jar used to install SymmetricDS
# This file must be in the Docker context (i.e. working directory)
ARG SETUP_JAR

WORKDIR /app
COPY ./auto-install.xml /app
COPY $SETUP_JAR /app
COPY README.md /app

# Install editors for easy configuration
RUN apk add --no-cache nano
RUN apk add --no-cache vim

# Install SymmetricDS
RUN java -jar $SETUP_JAR -console auto-install.xml

RUN rm -f $SETUP_JAR

ENV SYM_HOME /opt/symmetric-ds

# Create a volume containing the engines, tmp, conf, and security directories
VOLUME /opt/symmetric-ds/engines
VOLUME /opt/symmetric-ds/tmp
VOLUME /opt/symmetric-ds/conf
VOLUME /opt/symmetric-ds/security

EXPOSE 31415
EXPOSE 31417

CMD /opt/symmetric-ds/bin/sym_service start && tail -F /opt/symmetric-ds/logs/symmetric.log