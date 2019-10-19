FROM centos:8

RUN dnf update -y
RUN dnf -y install httpd

COPY 000-default.conf /etc/httpd/conf.d/000-default.conf

CMD ["/usr/sbin/httpd", "-DFOREGROUND"]
