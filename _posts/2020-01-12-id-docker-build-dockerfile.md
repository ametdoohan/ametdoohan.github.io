---
layout: post
title: "Membuat docker images dari dockerfile Part-1"
date: 2020-01-12 10:00:00 +0700
categories: docker
---

Tutorial ini akan membuat docker images lighttpd menggunakan alpine dari dockerfile.


Prerequisties :
- docker sudah terinstall
- text editor (ex: vi)

Berikut adalah step - nya

1. Tetapkan workdir untuk membuat dockerfile, (ex: /home/amet/lighttpd-alpine)

{% highlight bash %}
$ pwd
/home/amet/lighttpd-alpine
{% endhighlight %}

buat file dockerfile seperti berikut

{% highlight bash %}
$ cat dockerfile

# menggunakan image alpine
FROM alpine:latest

MAINTAINER amet doohan <ametdoohan@live.com>

LABEL version="1.0"
LABEL description="lighttpd running on port 80"

# expose pada port 80
EXPOSE 80

# install lighttpd dan konfigurasi (https://wiki.alpinelinux.org/wiki/Lighttpd)
RUN apk add --update --no-cache lighttpd && \
        rm -rf /var/cache/apk/* && \
        lighttpd -t -f /etc/lighttpd/lighttpd.conf && \
        echo "Lighttpd is running..." > /var/www/localhost/htdocs/index.html && \
        addgroup www && \
        adduser -D -H -s /sbin/nologin -G www www

# running lighttpd
ENTRYPOINT ["/usr/sbin/lighttpd", "-D", "-f", "/etc/lighttpd/lighttpd.conf"]

{% endhighlight %}

atau dapat pull dockerfile dari git saya
{% highlight bash %}
git pull https://github.com/ametdoohan/lighttpd-alpine-docker.git
{% endhighlight %}

{:start="2"}
2. Build image dengan docker build (docker build . -t namaimage:tag)

{% highlight bash %}
$ docker build . -t my_alpine_lighttpd:latest
{% endhighlight %}

{:start="3"}
3. Melihat image yang telah terbuat.

{% highlight bash %}
$ docker images

REPOSITORY           TAG                 IMAGE ID            CREATED              SIZE
my_alpine_lighttpd   latest              396e79d82866        About a minute ago   13.7MB
{% endhighlight %}

{:start="4"}
4. Running container menggunakan image yang telah dibuat, command dibawah running container pada port 8080

{% highlight bash %}
$ docker run -d -p 8080:80 --name my_web_server my_alpine_lighttpd:latest
{% endhighlight %}

{% highlight bash %}
$  docker ps
CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS              PORTS                  NAMES
c7cc9786f262        my_alpine_lighttpd:latest   "/usr/sbin/lighttpd …"   41 seconds ago      Up 40 seconds       0.0.0.0:8080->80/tcp   my_web_server
{% endhighlight %}

{:start="5"}
5. Cek apakah webserver telah running

{% highlight bash %}
$ curl http://localhost:8080
Lighttpd is running...
{% endhighlight %}

web server menggunakan lighttpd yang running pada image base alpine telah running! 

Sneak peek untuk Part-2:
- merubah htdocs sesuai keinginan (bind mounts).
- push docker image ke registry.