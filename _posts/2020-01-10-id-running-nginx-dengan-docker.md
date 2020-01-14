---
layout: post
title: "Running Nginx dengan Docker"
date: 2020-01-10 10:00:00 +0700
categories: docker
---

Ini adalah guide Running Nginx dengan Docker

Prerequisties :
- Docker sudah terinstall. [Install docker CE di CentOS 7 - [ID]](https://ametdoohan.github.io/id-docker-ce-install-centos7/)

berikut step running nginx dengan docker

1. Pull images nginx terbaru. (kecepatan tergantung koneksi kalian)

{% highlight bash %}
$ docker pull nginx:latest
{% endhighlight %}

Jika telah selesai, lihat images yang sudah di download

{% highlight bash %}
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              c7460dfcab50        30 hours ago        126MB
hello-world         latest              fce289e99eb9        12 months ago       1.84kB
{% endhighlight %}

{:start="2"}
2. Run container dengan image nginx yang sudah di pull. container akan dinamakan mycontainer dan running port 8080

{% highlight bash %}
$ docker run --name mycontainer -p 8080:80 nginx:latest
{% endhighlight %}

{:start="3"}
3. buka terminal baru untuk melihat apakah container running

{% highlight bash %}
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
b80639e011db        nginx:latest        "nginx -g 'daemon of…"   22 seconds ago      Up 21 seconds       0.0.0.0:8080->80/tcp   mycontainer
{% endhighlight %}

{% highlight bash %}
$ curl localhost:8080
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
{% endhighlight %}

Selamat, Running Nginx dengan Docker telah berhasil!.

tambahan, apabila ingin running container di background, dapat menggunakan option '-d' atau '--detach' pada step nomor 2

{% highlight bash %}
$ docker run -d --name mycontainer -p 8080:80 nginx:latest
{% endhighlight %}