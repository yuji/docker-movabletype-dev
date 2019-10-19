FROM centos:8

RUN dnf update -y

# Build Essentials
RUN dnf group install "Development Tools" -y

# Enable EPEL repository
RUN dnf install epel-release -y && \
    sed -i -e "s/enabled *= *1/enabled=0/g" /etc/yum.repos.d/epel.repo

# Install related libraries & headers
RUN dnf install -y openssl-devel
RUN dnf install -y libxml2-devel
RUN dnf install -y expat-devel

# Ready to install ImageMagick
RUN dnf config-manager --set-enabled PowerTools

RUN dnf --enablerepo=epel -y install ImageMagick
RUN dnf --enablerepo=epel -y install ImageMagick-devel
RUN dnf --enablerepo=epel -y install ImageMagick-perl

# Ready to instal Perl modules
RUN dnf install -y perl-App-cpanminus

RUN dnf install -y perl-DBI
RUN dnf install -y perl-DBD-MySQL
RUN dnf install -y perl-Archive-Tar
RUN dnf install -y perl-Archive-Zip
RUN dnf install -y perl-YAML-Syck
RUN dnf install -y perl-libwww-perl
RUN dnf install -y perl-Net-SSLeay
RUN dnf install -y perl-Test-Warn
RUN dnf install -y perl-CGI
RUN dnf install -y perl-HTTP-Daemon
RUN dnf install -y perl-Net-Server
RUN dnf install -y perl-LWP-Protocol-https
RUN dnf install -y perl-XML-LibXML

RUN cpanm Plack
RUN cpanm CGI::PSGI
RUN cpanm CGI::Parse::PSGI
RUN cpanm CGI::Compile
RUN cpanm Mozilla::CA
RUN cpanm XML::SAX::ExpatXS
RUN cpanm Authen::SASL
RUN cpanm Digest::SHA1
RUN cpanm Crypt::DSA
RUN cpanm Cache::File
RUN cpanm XML::SAX::Expat

RUN cpanm XMLRPC::Transport::HTTP::Plack --notest
RUN cpanm Starman --notest


# Okay, ready to run Movable Type
WORKDIR /app/mt

CMD ["starman", "--workers", "4", "--listen", ":5000", "--error-log", "/data/files/logs/mt/movabletype.log", "--pid", "/var/run/mt.pid", "mt.psgi"]
