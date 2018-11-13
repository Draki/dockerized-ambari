FROM danielrodriguez/docker-preambari

RUN apt-get install -y ambari-server && ambari-server setup -v -s
EXPOSE 8080

ADD scripts /root/scripts
ENTRYPOINT ["/root/scripts/start.sh"]