FROM ubuntu:16.04

RUN apt-get update && apt-get install -y wget apt-utils net-tools openssh-server

# Add key
RUN wget -O - http://packages.lizardfs.com/lizardfs.key | apt-key add -
RUN echo "deb http://packages.lizardfs.com/ubuntu/xenial xenial main" > /etc/apt/sources.list.d/lizardfs.list

RUN echo "172.20.0.2 mfsmaster" >> /etc/hosts

RUN apt-get update && apt-get install -y lizardfs-client
RUN mkdir -p /var/run/sshd
RUN echo "root:lizarddocker7" | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22
CMD mkdir -p /mnt/lizardfs && mfsmount -H lizardfs-master -o cacheexpirationtime=5000 -o mfswritecachesize=32 /mnt/lizardfs && /usr/sbin/sshd -D

