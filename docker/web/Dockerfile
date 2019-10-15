FROM centos:8

RUN yum update -y
RUN yum -y install httpd

COPY 000-default.conf /etc/httpd/conf.d/000-default.conf

CMD ["/usr/sbin/httpd", "-DFOREGROUND"]
