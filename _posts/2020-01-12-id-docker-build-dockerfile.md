---
layout: post
title: "Membuat docker images dari dockerfile - [ID]"
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

2. build image dengan docker build (docker build . -t namaimage:tag)

{% highlight bash %}
$ docker build . -t my_alpine_lighttpd:latest
{% endhighlight %}

{% highlight bash %}
Sending build context to Docker daemon  56.83kB
Step 1/7 : FROM alpine:latest
 ---> cc0abc535e36
Step 2/7 : MAINTAINER amet doohan <ametdoohan@live.com>
 ---> Using cache
 ---> 0421c900d735
Step 3/7 : LABEL version="1.0"
 ---> Using cache
 ---> 35aeb6b27334
Step 4/7 : LABEL description="lighttpd running on port 80"
 ---> Using cache
 ---> 9806a76e3eae
Step 5/7 : EXPOSE 80
 ---> Using cache
 ---> 65eb42126ae4
Step 6/7 : RUN apk add --update --no-cache lighttpd &&  rm -rf /var/cache/apk/* &&      lighttpd -t -f /etc/lighttpd/lighttpd.conf &&   echo "Lighttpd is running..." > /var/www/localhost/htdocs/index.html &&  addgroup www &&         adduser -D -H -s /sbin/nologin -G www www
 ---> Using cache
 ---> 28c2346a0fbb
Step 7/7 : ENTRYPOINT ["/usr/sbin/lighttpd", "-D", "-f", "/etc/lighttpd/lighttpd.conf"]
 ---> Using cache
 ---> 20be9f7d05b6
Successfully built 20be9f7d05b6
Successfully tagged my_alpine_lighttpd:latest
{% endhighlight %}