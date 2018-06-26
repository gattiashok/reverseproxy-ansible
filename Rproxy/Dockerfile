FROM centos:7
MAINTAINER "Ashok Kumar"<ashok.g@gmail.com>
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]
RUN yum install epel-release -y && rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
RUN yum --enablerepo=remi-php72 install php -y
RUN yum -y install httpd httpd-devel; yum clean all; systemctl enable httpd.service
COPY /httpd.conf /etc/httpd/conf
RUN yum install firewalld -y && systemctl enable firewalld
RUN yum install nginx -y
COPY /demo.conf /etc/nginx/conf.d
RUN  systemctl enable nginx
RUN yum install make gcc automake zlib-devel bison cmake libtool wget gcc-c++ unzip ncurses-devel openssl-devel pcre-devel libxml2-devel curl-devel gd-devel libxslt- devel libjpeg-devel -y
ADD "http://mirror.trouble-free.net/sources/mod_rpaf-0.6.tar.gz" /root
WORKDIR /root
RUN tar zxvf mod_rpaf-0.6.tar.gz
WORKDIR /root/mod_rpaf-0.6
RUN cp mod_rpaf-2.0.c mod_rpaf-2.4.c && sed -i 's/remote_/client_/g' mod_rpaf-2.4.c && apxs -c -n mod_rpaf-2.4.so mod_rpaf-2.4.c && apxs -i -c -n mod_rpaf-2.4.so mod_rpaf-2.4.c
EXPOSE 80
CMD ["/usr/sbin/init"]