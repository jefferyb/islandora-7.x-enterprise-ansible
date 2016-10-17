# To build, do:
#   $ docker build -t islandora-mysql --pull .
#
# To run, do:
#   $ docker run -d --name islandora-mysql-server -p 3306:3306 islandora-mysql

FROM jefferyb/ansible:trusty
MAINTAINER Jeffery Bagirimvano <jefferyb@uark.edu>

ENV MYSQL_ROOT_PASSWORD="islandora"
ENV FEDORA_DATABASE_NAME="fedora3"
ENV FEDORA_DATABASE_USER="fedoraAdmin"
ENV FEDORA_DATABASE_PASSWORD="islandora"
ENV FGSADMIN_USER="fgsAdmin"
ENV FGSADMIN_PASSWORD="islandora"
ENV DRUPAL_DATABASE_NAME="drupal7"

RUN \
    mkdir -p /playbooks
    git clone clone -b docker-install https://github.com/jefferyb/islandora-7.x-enterprise-ansible.git /playbooks/islandora-7.x-Enterprise && \
    cd /playbooks/islandora-7.x-Enterprise && \

    echo '---\n\
- hosts: localhost\n\
  roles:\n\
    - islandora-mysql\n\
\n'\
>> install-islandora-mysql.yaml && \

    ansible-playbook install-islandora-mysql.yaml && \

VOLUME /playbooks
VOLUME /var/lib/mysql

WORKDIR /playbooks/islandora-7.x-Enterprise

EXPOSE 3306

CMD ["mysqld"]
