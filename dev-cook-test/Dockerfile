FROM centos

RUN yum install -y passwd
RUN yum install -y openssh
RUN yum install -y openssh-server
RUN yum install -y openssh-clients
RUN yum install -y sudo

## create user
RUN useradd vagrant
RUN passwd -f -u vagrant
RUN mkdir -p /home/vagrant/.ssh; chown vagrant /home/vagrant/.ssh; chmod 700 /home/vagrant/.ssh
ADD ./authorized_keys /home/vagrant/.ssh/authorized_keys
RUN chown vagrant /home/vagrant/.ssh/authorized_keys; chmod 600 /home/vagrant/.ssh/authorized_keys

## setup sudoers
RUN echo "vagrant ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/vagrant

# sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config

# sudoers
RUN sed -ri 's/Defaults +requiretty/#Defaults requiretty/g' /etc/sudoers

## setup sshd and generate ssh-keys by init script
RUN /etc/init.d/sshd start
RUN /etc/init.d/sshd stop


## Seems we cannnot fix public port number
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
