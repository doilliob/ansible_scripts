FROM ubuntu:latest
RUN apt update && \
    apt install software-properties-common -y && \
    apt-add-repository --yes --update ppa:ansible/ansible && \
    apt install ansible cron -y
RUN mkdir /ansible

COPY *.yaml /ansible/

RUN mkdir -p /root/.ssh

COPY known_hosts /root/.ssh/

RUN mkdir -p /mnt/backup/site/daily && \
    mkdir -p  /mnt/backup/sdo && \
    mkdir -p /mnt/backup/configurations

COPY jobs /etc/cron.d/jobs

RUN chmod 0644 /etc/cron.d/jobs

RUN crontab /etc/cron.d/jobs

RUN touch /var/log/cron.log

CMD cron && tail -f /var/log/cron.log
 

