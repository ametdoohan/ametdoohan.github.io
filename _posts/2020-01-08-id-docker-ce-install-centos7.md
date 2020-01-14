---
layout: post
title: "Install docker CE di CentOS 7"
date: 2020-01-08 10:00:00 +0700
categories: docker
---

Ini adalah guide untuk install Docker CE di CentOS7

Prerequisties :
- CentOS 7
- User account yang mempunyai sudo privileges
- Akses SSH ke server tersebut
- CentOS Extras repository

Install menggunakan repository docker-ce.repo

1. Install Package yang dibutuhkan.

{% highlight bash %}
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
{% endhighlight %}

{:start="2"}
2. Setup stable repository.

{% highlight bash %}
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
{% endhighlight %}

{:start="3"}
3. Install latest version Docker Engine - Community

{% highlight bash %}
sudo yum install -y docker-ce docker-ce-cli containerd.io
{% endhighlight %}

{:start="4"}
4. Start docker Services

{% highlight bash %}
sudo systemctl start docker
{% endhighlight %}

{:start="5"}
5. Enable automatically start on boot

{% highlight bash %}
sudo systemctl enable docker
{% endhighlight %}

{:start="6"}
6. Verifikasi test bahwa Docker CE sudah terinstall

{% highlight bash %}
sudo docker run hello-world
{% endhighlight %}

Jika berhasil maka hasilnya seperti berikut

{% highlight bash %}
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete
Digest: sha256:d1668a9a1f5b42ed3f46b70b9cb7c88fd8bdc8a2d73509bb0041cf436018fbf5
Status: Downloaded newer image for hello-world:latest

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

 Selamat, Install docker CE di CentOS 7 telah berhasil!