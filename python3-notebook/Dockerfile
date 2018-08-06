#FROM ubuntu@sha256:84c334414e2bfdcae99509a6add166bbb4fa4041dc3fa6af08046a66fed3005f
FROM jupyter/base-notebook

LABEL maintainer="Jing Wang <jingwangian@gmail.com>"

USER root

RUN apt-get update \
    && apt-get -y install openssh-server \
    && apt-get install -yq openssh-client

RUN apt-get install -yq vim man

RUN mkdir /var/run/sshd

EXPOSE 22
RUN sed -i '/PermitRootLogin/c\PermitRootLogin yes' /etc/ssh/sshd_config

WORKDIR /home/$NB_USER/node
RUN mkdir src

COPY entrypoint.sh conf/

RUN chown -R $NB_USER:$NB_GID /home/$NB_USER/node

RUN echo root:rootpasswd |chpasswd
RUN echo $NB_USER:nopasswd |chpasswd
RUN usermod -aG sudo $NB_USER

RUN chmod u+x /etc/sudoers \
    && echo "$NB_USER ALL=NOPASSWD: ALL" >>/etc/sudoers \
    && chmod u-x /etc/sudoers

# switch user
USER $NB_USER

# copy ssh keys
RUN mkdir -p /home/$NB_USER/node/keys \
    mkdir -p ~/.ssh
COPY keys/id_rsa_docker.pub /home/$NB_USER/node/keys/
RUN cat /home/$NB_USER/node/keys/id_rsa_docker.pub >> ~/.ssh/authorized_keys

VOLUME /home/$NB_USER/node/src

ENTRYPOINT ["conf/entrypoint.sh"]
#ENTRYPOINT ["/bin/bash"]
