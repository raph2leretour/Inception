# syntax=docker/dockerfile:1

FROM debian:bookworm

EXPOSE 3306

LABEL maintainer="Raphael TISSERAND <rtissera@student.42.fr>"

RUN <<EOF
apt-get update
apt-get dist-upgrade -y
apt-get install mariadb-server -y
apt-get clean
rm -rf /var/lib/apt/lists/*
mkdir -p /etc/mariadb /etc/mysql
EOF

COPY ./tools/myscript.sh /etc/mariadb/myscript.sh
COPY ./conf/my.cnf /etc/mysql/my.cnf

RUN <<EOF
sed -i s/^bind-address.*$/bind-address = 0.0.0.0/g /etc/mysql/mariadb.conf.d/50-server.cnf
chmod u+x /etc/mariadb/myscript.sh
EOF

ENTRYPOINT ["/etc/mariadb/myscript.sh"]
