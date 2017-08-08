FROM ubuntu:16.04

RUN apt-get update && apt-get install -y wget apt-utils net-tools openssh-server

# Add key
RUN wget -O - http://packages.lizardfs.com/lizardfs.key | apt-key add -
RUN echo "deb http://packages.lizardfs.com/ubuntu/xenial xenial main" > /etc/apt/sources.list.d/lizardfs.list

RUN apt-get update && apt-get install -y lizardfs-master lizardfs-cgi*

EXPOSE 9420 9421 9422 9423 9424 9425 22

RUN cp /var/lib/mfs/metadata.mfs.empty /var/lib/mfs/metadata.mfs
RUN cp /etc/mfs/mfsexports.cfg.dist /etc/mfs/mfsexports.cfg
RUN cp /etc/mfs/mfsmaster.cfg.dist /etc/mfs/mfsmaster.cfg
RUN echo "MASTER_HOST=lizardfs-master" >> /etc/mfs/mfsmaster.cfg

RUN sed -i "s/fals/tru/g" /etc/default/lizardfs-cgiserv
RUN sed -i "s/fals/tru/g" /etc/default/lizardfs-master
RUN echo "root:lizarddocker7" | chpasswd
RUN mkdir -p /var/run/sshd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

CMD service lizardfs-cgiserv start && service lizardfs-master start && /usr/sbin/sshd -D

