FROM tomcat:8.5.42-jdk8-openjdk

MAINTAINER Maven Shark LLC <mark.havens@mavenshark.com>

WORKDIR $CATALINA_HOME

ENV OPENMAINT_URL https://sourceforge.net/projects/cmdbuild/files/3.1.1/cmdbuild-3.1.1.war/download
ENV POSTGRES_USER postgres
ENV POSTGRES_PASS postgres
ENV POSTGRES_PORT 5432
ENV POSTGRES_HOST openmaint_db
ENV POSTGRES_DB openmaint_db3
ENV OPENMAINT_DUMP empty

RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
    maven \
	postgresql-client

RUN set -x \
 	&& mkdir $CATALINA_HOME/conf/openmaint/ \
 	&& mkdir $CATALINA_HOME/webapps/openmaint/

COPY files/tomcat-users.xml $CATALINA_HOME/conf/tomcat-users.xml
COPY files/context.xml $CATALINA_HOME/webapps/manager/META-INF/context.xml
COPY files/database.conf $CATALINA_HOME/conf/openmaint/database.conf
COPY files/docker-entrypoint.sh /usr/local/bin/


RUN set -x \
	&& groupadd tomcat \
	&& useradd -s /bin/false -g tomcat -d $CATALINA_HOME tomcat \
	&& cd /tmp \
	&& wget -O openmaint.war "$OPENMAINT_URL" \
	&& chmod 777 openmaint.war \
	&& chmod 777 /usr/local/bin/docker-entrypoint.sh \
	&& unzip openmaint.war -d openmaint \
	&& mv openmaint.war $CATALINA_HOME/webapps/openmaint.war \
	&& mv openmaint/* $CATALINA_HOME/webapps/openmaint/ \
	&& chmod 777 $CATALINA_HOME/webapps/openmaint/openmaint.sh \
	&& chown tomcat -R $CATALINA_HOME \
	&& cd /tmp \
	&& rm -rf * \
	&& rm -rf /var/lib/apt/lists/*

# cleanup
RUN apt-get -qy autoremove

ENTRYPOINT /usr/local/bin/docker-entrypoint.sh

USER tomcat

EXPOSE 8080

CMD ["catalina.sh", "run"]
