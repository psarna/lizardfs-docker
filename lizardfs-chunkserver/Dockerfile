FROM ubuntu:16.04

RUN apt-get update && apt-get install -y wget apt-utils net-tools openssh-server

# Add key
RUN wget -O - http://packages.lizardfs.com/lizardfs.key | apt-key add -
RUN echo "deb http://packages.lizardfs.com/ubuntu/xenial xenial main" > /etc/apt/sources.list.d/lizardfs.list

RUN apt-get update && apt-get install -y lizardfs-chunkserver

EXPOSE 9419 9420 9422 22

RUN cp /etc/mfs/mfschunkserver.cfg.dist /etc/mfs/mfschunkserver.cfg
RUN echo "MASTER_HOST=lizardfs-master" >> /etc/mfs/mfschunkserver.cfg
RUN mkdir -p /mnt/sdb1
RUN chown -R mfs. /mnt/sdb1
RUN echo "/mnt/sdb1" >> /etc/mfs/mfshdd.cfg
RUN sed -i '/# LABEL = _/c\LABEL = docker' /etc/mfs/mfschunkserver.cfg
RUN sed -i "s/fals/tru/g" /etc/default/lizardfs-chunkserver
RUN echo "root:lizarddocker7" | chpasswd
RUN mkdir -p /var/run/sshd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

CMD service lizardfs-chunkserver start && /usr/sbin/sshd -D

