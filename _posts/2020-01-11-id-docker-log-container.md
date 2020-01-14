---
layout: post
title: "Log nginx container pada Docker"
date: 2020-01-11 10:00:00 +0700
categories: docker
---

Ini adalah guide log nginx container pada docker

Prerequisties :
- Running nginx dengan docker [Here.](https://ametdoohan.github.io/id-running-nginx-dengan-docker/)

berikut command log container pada docker

1. docker logs running nginx

{% highlight bash %}
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
b80639e011db        nginx:latest        "nginx -g 'daemon of…"   25 minutes ago      Up 7 minutes        0.0.0.0:8080->80/tcp   mycontainer

$ docker logs -f mycontainer
{% endhighlight %}

{:start="2"}
2. Test hit port 8080 (port expose container nginx)

{% highlight bash %}
$ curl http://your-ip-address:8080
{% endhighlight %}

{:start="3"}
3. Lihat kembali terminal log (step no.1)

{% highlight bash %}
$ docker logs -f mycontainer
172.17.0.1 - - [11/Jan/2020:04:51:33 +0000] "GET / HTTP/1.1" 200 612 "-" "curl/7.29.0" "-"
172.17.0.1 - - [11/Jan/2020:04:51:35 +0000] "GET / HTTP/1.1" 200 612 "-" "curl/7.29.0" "-"
172.17.0.1 - - [11/Jan/2020:05:13:52 +0000] "GET / HTTP/1.1" 200 612 "-" "curl/7.29.0" "-"
192.168.1.2 - - [11/Jan/2020:05:14:07 +0000] "GET / HTTP/1.1" 200 612 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.117 Safari/537.36" "-"
2020/01/11 05:14:07 [error] 6#6: *2 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 192.168.1.2, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "192.168.1.6:8080", referrer: "http://192.168.1.6:8080/"
192.168.1.2 - - [11/Jan/2020:05:14:07 +0000] "GET /favicon.ico HTTP/1.1" 404 555 "http://192.168.1.6:8080/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.117 Safari/537.36" "-"
{% endhighlight %}

log container dapat terbaca.