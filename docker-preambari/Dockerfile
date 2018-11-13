FROM ubuntu:16.04

# python-dev
#    && apt-get install -q -y --no-install-recommends wget scp curl unzip tar openssl python2.7 gcc zlibc postgresql-server ntp \
# apt openssh-server openssh-client
RUN apt-get -qq update && apt-get -y -qq upgrade \
    && apt-get install -q -y --no-install-recommends wget ntp curl python2.7 openssl unzip tar ufw ssh net-tools \
#    && apt-get install -q -y --no-install-recommends wget ntp curl python net-tools inetutils-ping ssh vim telnet lsof less -y
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


# Add HDP and Ambari repos

RUN wget -O /etc/apt/sources.list.d/ambari.list http://public-repo-1.hortonworks.com/ambari/ubuntu16/2.x/updates/2.7.1.0/ambari.list
RUN wget -O /etc/apt/sources.list.d/hdp.list http://public-repo-1.hortonworks.com/HDP/ubuntu16/3.x/updates/3.0.1.0/hdp.list

#RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B9733A7A07513CAD
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B9733A7A07513CAD
RUN apt-get update


# Set up SSH

#RUN ssh-keygen
#RUN cat id_rsa.pub >> authorized_keys
#RUN chmod 700 ~/.ssh \
#    && chmod 600 ~/.ssh/authorized_keys

RUN mkdir /root/.ssh && mkdir /root/scripts && mkdir /root/config

ADD config/id_rsa /root/.ssh/id_rsa
ADD config/id_rsa.pub /root/.ssh/id_rsa.pub
RUN sed -i 's/#AuthorizedKeysFile/AuthorizedKeysFile/g' /etc/ssh/sshd_config

RUN touch /root/.ssh/authorized_keys \
    && cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys \
    && chmod -R 600 /root/.ssh/

ADD config/hosts /etc/



#From the Ambari Server, make sure you can connect to each host in the cluster using SSH, without having to enter a password.#
#ssh root@<remote.target.host>#
#where <remote.target.host> has the value of each host name in your cluster.#

#If the following warning message displays during your first connection: Are you sure you want to continue connecting (yes/no)? Enter Yes.#
#
#RUN ufw disable \
#    && iptables -X \
#    && iptables -t nat -F \
#    && iptables -t nat -X \
#    && iptables -t mangle -F \
#    && iptables -t mangle -X \
#    && iptables -P INPUT ACCEPT \
#    && iptables -P FORWARD ACCEPT \
#    && iptables -P OUTPUT ACCEPT
#RUN setenforce 0
#    && echo umask 0022 >> /etc/profile

##en el bootstrap
# update-rc.d ntp defaults
#sudo ufw disable
#sudo iptables -X
#sudo iptables -t nat -F
#sudo iptables -t nat -X
#sudo iptables -t mangle -F
#sudo iptables -t mangle -X
#sudo iptables -P INPUT ACCEPT
#sudo iptables -P FORWARD ACCEPT
#sudo iptables -P OUTPUT ACCEPT
#
#apt-get install ambari-server
#ambari-server setup -s