---
layout: post
title: "Push image ke docker hub Part-2"
date: 2020-01-13 10:00:00 +0700
categories: docker
---

Tutorial ini akan pull image ke docker hub, dan tutorial ini adalah lanjutan dari [Membuat docker images dari dockerfile Part-1
](https://ametdoohan.github.io/id-docker-build-dockerfile/)


Prerequisties :
- docker sudah terinstall
- sudah punya docker image sendiri, [example](https://ametdoohan.github.io/id-docker-build-dockerfile/)
- mempunyai akun [Docker ID](https://hub.docker.com/signup) 

Berikut adalah step - nya

1. Cek image yang ada di localhost. Image yang saya punya adalah 'my_alpine_lighttpd'

{% highlight bash %}
$ docker images
REPOSITORY           TAG                 IMAGE ID            CREATED             SIZE
my_alpine_lighttpd   latest              396e79d82866        4 hours ago         13.7MB
{% endhighlight %}

{:start="2"}
2. Login menggunakan Docker ID

{% highlight bash %}
$ docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: YOUR_USERNAME
Password: YOUR_PASSWORD
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
{% endhighlight %}

{:start="3"}
3. Tag image yang sudah dibuat " 'docker tag 'IMAGE ID' 'Dockerhub Username'/'nama image:nama tag' "

{% highlight bash %}
$ docker tag 396e79d82866 ametdoohan/my_alpine_lighttpd:latest
{% endhighlight %}

{:start="4"}
4. Push image ke repository docker hub

{% highlight bash %}
$ docker push ametdoohan/my_alpine_lighttpd
The push refers to repository '[docker.io/ametdoohan/my_alpine_lighttpd]'
27c27a5defc0: Pushed
6b27de954cca: Mounted from ametdoohan/lighttpd-alpine
latest: digest: sha256:91c4f797c20587eaa796c0df6cdf6ac484669f083612bff36f2c1530d38caa25 size: 739
{% endhighlight %}

Image yang dibuat sudah dapat diakses pada [Docker Hub](https://hub.docker.com/) kalian, untuk pull image yang sudah ada di docker hub berikut command nya.

{% highlight bash %}
$ docker push ametdoohan/my_alpine_lighttpd:latest
{% endhighlight %}

maka image akan ada di localhost kita.

{% highlight bash %}
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE

$ docker pull ametdoohan/my_alpine_lighttpd:latest
latest: Pulling from ametdoohan/my_alpine_lighttpd
e6b0cf9c0882: Pull complete
56f77ec2dc6e: Pull complete
Digest: sha256:91c4f797c20587eaa796c0df6cdf6ac484669f083612bff36f2c1530d38caa25
Status: Downloaded newer image for ametdoohan/my_alpine_lighttpd:latest
docker.io/ametdoohan/my_alpine_lighttpd:latest

$ docker images
REPOSITORY                      TAG                 IMAGE ID            CREATED             SIZE
ametdoohan/my_alpine_lighttpd   latest              396e79d82866        5 hours ago         13.7MB
{% endhighlight %}

Tutorial ini telah selesai! Part-3 akan melakukan bind mounts pada docker.