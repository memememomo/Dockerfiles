FROM centos

RUN yum -y update
RUN yum -y install telnet ftp nmap unzip libxml2-devel curl-devel gd-devel git gitflow libxslt-devel lsof bind-utils libaio-devel

RUN yum install -y sysstat
RUN /etc/init.d/sysstat start

RUN yum install -y ntp
ADD ./ntpdate.sh /etc/cron.hourly/ntpdate.sh
ADD ./clock /etc/sysconfig/clock
RUN ntpdate -s ntp.nict.jp
RUN mv /etc/localtime /etc/localtime.org
RUN ln -s /usr/share/zoneinfo/Japan /etc/localtime

EXPOSE 80
EXPOSE 3306
EXPOSE 22
