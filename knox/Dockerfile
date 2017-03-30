FROM openjdk:8-jre-alpine

MAINTAINER sumitg

RUN apk --no-cache add bash procps
RUN adduser -S knox

ENV KNOX_VERSION 0.12.0

RUN wget -q -O /knox-${KNOX_VERSION}.zip http://download.nextag.com/apache/knox/${KNOX_VERSION}/knox-${KNOX_VERSION}.zip && unzip /knox-${KNOX_VERSION}.zip && rm knox-${KNOX_VERSION}.zip && ln -nsf /knox-${KNOX_VERSION} /knox && chmod +x /knox/bin/*.sh && chown -R knox /knox/

#ADD master /knox/data/security/master
RUN /knox/bin/knoxcli.sh create-master --master knox
RUN chown -R knox /knox/data/security

ADD ldap.sh /knox/bin/ldap.sh
ADD gateway.sh /knox/bin/gateway.sh
ADD goodloans-auth.zip /knox/data/applications/goodloans-auth.zip
ADD unwise-auth.zip /knox/data/applications/unwise-auth.zip
ADD goodloans-sso.xml /knox/conf/topologies/goodloans-sso.xml
ADD goodloans.xml /knox/conf/topologies/goodloans.xml
ADD unwise-sso.xml /knox/conf/topologies/unwise-sso.xml
ADD unwise.xml /knox/conf/topologies/unwise.xml

RUN cd /knox/data/applications && unzip goodloans-auth.zip && unzip unwise-auth.zip && chown -R knox /knox/


USER knox
WORKDIR /knox
