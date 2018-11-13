FROM danielrodriguez/docker-preambari

RUN apt-get install -y ambari-agent
RUN sed -i '/^hostname=.*$/c\hostname=ambari' /etc/ambari-agent/conf/ambari-agent.ini

ADD scripts /root/scripts
ENTRYPOINT ["/root/scripts/start.sh"]