FROM ubuntu:22.04

WORKDIR /build

COPY main.c .

RUN apt update -y && \
    apt install -y nginx libfcgi-dev gcc spawn-fcgi curl && \
    useradd -r nginx && \
    chmod u-s /usr/bin/umount /usr/bin/chsh /usr/bin/su /usr/bin/gpasswd /usr/bin/passwd /usr/bin/mount /usr/bin/newgrp>    chmod g-s /usr/bin/expiry /usr/sbin/pam_extrausers_chkpwd /usr/sbin/unix_chkpwd /usr/bin/wall /usr/bin/chage && \
    rm -rf /var/lib/apt/lists/*

COPY nginx/nginx.conf /etc/nginx/nginx.conf

HEALTHCHECK --interval=5m --timeout=3s CMD curl -f http://localhost/ || exit 1

USER nginx

ENTRYPOINT gcc -o main main.c -lfcgi && spawn-fcgi -p 8080 main && service nginx start && tail -f /dev/null