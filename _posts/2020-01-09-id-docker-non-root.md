---
layout: post
title: "Running Docker sebagai User - [ID]"
date: 2020-01-09 10:00:00 +0700
categories: docker
---

Ini adalah guide running docker sebagai user non Root

1. Untuk run Docker sebagai non-root user, kita harus memasukan user tersebut kedalam grup docker.

{% highlight bash %}
sudo cat /etc/group | grep docker
docker:x:995:
{% endhighlight %}

{:start="2"}
2. Jika grup docker belum ada, buat grup tersebut.

{% highlight bash %}
sudo group add docker
{% endhighlight %}

{:start="3"}
3. Tambahkan user kedalam grup docker

{% highlight bash %}
sudo usermod -aG docker [non-root-user]
{% endhighlight %}

{:start="4"}
4. Verifikasi run docker tanpa root akses

{% highlight bash %}
docker run hello-world
{% endhighlight %}

Jika berhasil maka hasilnya seperti berikut

{% highlight bash %}
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

 {% endhighlight %}

 Selamat, Running Docker sebagai User telah berhasil!