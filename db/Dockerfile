FROM mysql:5.7
LABEL maintainer="Ivan Blancas <ibr272515@gmail.com>"

# Declare variables
ENV TZ=America/Mexico_City
ENV MYSQL_DATABASE: LPURLS
ENV MYSQL_USER: lpurlsuser
ENV MYSQL_PASSWORD: lpurlspasswd
ENV MYSQL_ROOT_USER: root
ENV MYSQL_ROOT_PASSWORD: lpurlspasswd

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install Apache, write ServerName and copy the SRC directory
RUN rm -rf /var/www/*
ADD src /var/www/html
RUN echo ServerName ${HOSTNAME} >> /etc/apache2/apache2.conf

# Install PHP Extensions
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install php libapache2-mod-php php-mysql 
ADD config/dir.conf /etc/apache2/mods-enabled/dir.conf

# Configure Apache to run with Docker
RUN echo '. /etc/apache2/envvars' > /root/run_apache.sh
RUN echo 'mkdir -p /var/run/apache2' >> /root/run_apache.sh
RUN echo 'mkdir -p /var/lock/apache2' >> /root/run_apache.sh
RUN echo '/usr/sbin/apache2 -D FOREGROUND' >> /root/run_apache.sh
RUN chmod 755 /root/run_apache.sh

EXPOSE 3306