FROM ubuntu:16.04

# Install required packages
RUN apt-get update && apt-get install -y openssh-server

# Create user
RUN mkdir /home/docker_root && \
    groupadd --gid 1001 docker_root && \
    useradd --uid 1001 -g 1001 --shell /bin/bash -d /home/docker_root docker_root && \
    chown docker_root.docker_root /home/docker_root && \
    mkdir /var/run/sshd

USER docker_root
RUN test -f /home/docker_root/.ssh/id_rsa || mkdir /home/docker_root/.ssh; \
    chmod 744 /home/docker_root/.ssh; ssh-keygen -t rsa -b 4096 -C "docker_root@example.com" -f /home/docker_root/.ssh/id_rsa -q -N ""; \
    cat /home/docker_root/.ssh/id_rsa.pub >> /home/docker_root/.ssh/authorized_keys

EXPOSE 22

USER root
CMD ["/usr/sbin/sshd", "-D"]
