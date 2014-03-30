FROM ubuntu:12.10
MAINTAINER Masami Yonehara <zeitdiebe@gmail.com>

# Because docker replaces /sbin/init: https://github.com/dotcloud/docker/issues/1024
#RUN dpkg-divert --local --rename --add /sbin/initctl
#RUN ln -s /bin/true /sbin/initctl

RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get -y install mysql-server
ADD ./my.cnf /etc/mysql/my.cnf
RUN rm /var/lib/mysql/ib_logfile* # Because new my.cnf is modified about innodb_log_file_size, it must be removed until starting mysqld.

RUN /usr/bin/mysqld_safe & \
    sleep 10s && \
    mysql -e "GRANT ALL ON *.* to 'root'@'%' IDENTIFIED BY ' **** FILL YOUR PASS **** '; FLUSH PRIVILEGES"

EXPOSE 3306

VOLUME ["/var/lib/mysql", "/var/log/mysql"]

CMD ["mysqld_safe"]
