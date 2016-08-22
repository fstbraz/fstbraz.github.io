---
layout: post
title: "Laravel Homestead on Mac osx"
date: 2016-02-06
excerpt: "With a perfect dev enviroment in mind, I've decided to get my hands on Laravel Homestead."
tags: [laravel, homestead, vagrant, virtual machine]
feature: /assets/img/fulls/03.jpg
comments: true
---

With a perfect dev enviroment in mind, I've decided to get my hands on [Laravel Homestead](https://laravel.com/docs/5.1/homestead), because it's a complete and easy configurable LEMP virtual machine that run's on [Vagrant](https://www.vagrantup.com/), so what you see next is a little guide how to configure and run a Homestead machine on Mac Osx 10.10.5.

### 1. Install VirtualBox and Vagrant

Before configure Homestead enviroment, we have to install [VirtualBox](https://www.virtualbox.org/wiki/Downloads) and [Vagrant](http://www.vagrantup.com/downloads.html). 


### 2. Add the Homestead Vagrant Box

After we install VirtualBox and Vagrant, we have to add the Homestead box to Vagrant, for doing that we can start by typing this on the mac osx terminal in the root directory:

> vagrant box add laravel/homestead

The download has started.
If it fails you can try with the next command:

> vagrant box add laravel/homestead https://atlas.hashicorp.com/laravel/boxes/homestead

After the Homestead is cloned in your machine, run the next command from the Homestead directory to create the `Homestead.yaml` configuration file, the file will be placed on the ~/.homestead hidden directory:

> bash init.sh
 

### 3. Configuring Homestead

The next step is set the key for the provider in the `~/.homestead/Homestead.yaml` (if is not set already automatically), we are using virtualbox, so it must be:

> provider: virtualbox

We have to configure the shared folders and the sites to:

{% highlight ruby %}

folders:
    - map: ~/file-of-my-projects/Laravel
      to: /home/vagrant/Code

sites:
    - map: homestead.app
      to: /home/vagrant/file-of-my-projects/Laravel/public

{% endhighlight %}

If you do any change to `sites`, like adding a new site, you should reload the Homestead Nginx configuration by runnig:

> vagrant reload --provision


### 4. Create the SSH key

In this step we have to provide the path on the `Homestead.yaml`, but first we have to create the key:

> ssh-keygen -t rsa -C "**yourname**@homestead"

Now we provide the path on `Homestead.yaml`, like:

{% highlight ruby %}

authorize: ~/.ssh/id_rsa.pub

keys:
    - ~/.ssh/id_rsa

{% endhighlight %}


### 5. Add the Nginx domain to your `hosts` file:

Go to you hosts files, on Mac should be on:

> sudo nano /etc/hosts 

And add this line :

> 192.168.10.10  homestead.app


### 6. Botting the Vagrant box

After we edit `hosts` and `Homestead.yaml`, we go to the Homestead directory and run:

> vagrant up

Vagrant will start, will take a will booting up, if any misconfiguration exists you can destroy the machine running:

> vagrant destroy


### 7. Setting up the Laravel project inside the Vagrant box

After all is booted up, we can connect to homestead machine doing:

> vagrant ssh

Now we head to our shared directory doing:

> cd file-of-my-projects

After that, we can pull a fresh project with composer:

> composer create-project --prefer-dist laravel/laravel Laravel

Go to `homestead.app` in your browser, if you could see the the Laravel 5 page, you are ready to start coding your webapp.
