# To build, do:
#   $ docker build -t islandora-fedora --pull .
#
# To run, do:
#   $ docker run -d --name islandora-fedora-server -p 8080:8080 islandora-fedora

FROM jefferyb/ansible:trusty
MAINTAINER Jeffery Bagirimvano <jefferyb@uark.edu>

# MySQL Settings:
ENV MYSQL_HOSTNAME="islandora-mysql"
ENV MYSQL_PORT=3306
ENV DRUPAL_DATABASE_NAME="drupal7"
ENV MYSQL_ROOT_USER="root"
ENV MYSQL_ROOT_PASSWORD="islandora"
ENV FEDORA_DATABASE_NAME="fedora3"
ENV FEDORA_DATABASE_USER="fedoraAdmin"
ENV FEDORA_DATABASE_PASSWORD="islandora"

ENV FGSADMIN_USER="fgsAdmin"
ENV FGSADMIN_PASSWORD="islandora"

# Tomcat Settings:
ENV TOMCAT_HOME="/var/lib/tomcat7"
ENV TOMCAT_USER="tomcat7"
ENV JAVA_HOME="/usr/lib/jvm/java-8-oracle/jre"

# Fedora Settings:
ENV FEDORA_HOME="/usr/local/fedora"
ENV FEDORA_VERSION=3.8.1
ENV FEDORA_HOSTNAME="localhost"

# Djatoka Settings:
ENV DJATOKA_HOME="/usr/local/djatoka"
ENV DJATOKA_HOSTNAME="localhost"


RUN \
    mkdir -p /playbooks && \
    git clone -b docker-install https://github.com/jefferyb/islandora-7.x-enterprise-ansible.git /playbooks/islandora-7.x-Enterprise && \
    cd /playbooks/islandora-7.x-Enterprise && \

    echo '---\n\
- hosts: localhost\n\
  roles:\n\
    - islandora-fedora\n\
\n'\
>> install-islandora-fedora.yaml && \

    echo '---\n\
- hosts: localhost\n\
  roles:\n\
    - start-fedora\n\
\n'\
>> start-fedora.yaml && \

    ansible-playbook install-islandora-fedora.yaml

VOLUME /playbooks
VOLUME ${FEDORA_HOME} ${TOMCAT_HOME}

WORKDIR /playbooks/islandora-7.x-Enterprise

EXPOSE 8080

CMD \
    ansible-playbook start-fedora.yaml && \
    tail -f /var/logs/tomcat7/catalina.out

