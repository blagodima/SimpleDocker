FROM ubuntu:22.04

WORKDIR build

COPY main.c .

RUN apt update -y && apt install -y nginx && apt-get install libfcgi-dev -y && apt-get -y install gcc && apt-get -y install spawn-fcgi && apt install -y curl && useradd -r nginx

COPY nginx/nginx.conf /etc/nginx/nginx.conf

ENTRYPOINT gcc -o main main.c -lfcgi && spawn-fcgi -p 8080 main && service nginx start && curl localhost:81
