---
layout: post
title: "Installing Python on Mac osx"
date: 2016-09-13
excerpt: "When trying to learn python, the first step is to set up the best dev enviroment."
tags: [python, mac, osx, virtual enviroment]
feature: /assets/img/fulls/03.jpg
comments: true
---

El Capitan already ships with a version of Python that is great for learning but it's not good for development. 
So for learning Python, in a stable way, first you have to set up your dev enviroment, what you see next is the complete set up to put python 2.7 rocking on Mac osx El Capitan. 

### 1. [Installing Homebrew](http://brew.sh/)

(If you have this awesome package manager installed and configured, you can skip this step).

> /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"


### 2. Installing Python

Now you can just simple install Python:

> brew install python

The download has started.
The installation will be complete in two minutes.
 

### 3. Setuptool e Pip configuration

Homebrew automatically set up and install Setuptools e Pip. 

Setuptolls lets you install and download any compatible and compliant Python software with a nice command `easy_install`. Also it can enables network installation capability to your own Python software with a few lines of code.

Pip is like a superior package manager for Python, that is more recommended an actively maintained than `easy_install`.


### 4. Virtual Enviroments

A virtual enviroment is a Python tool to keep the dependecies of the different projects in diferent places, by using virtual generated enviroments for them. It's the problem solver for version conflicts and keeps global site packages clean and in order.  

We can start to install the virtual env via pip:

> pip install virtualenv

Now we can create a directory and a virtual enviroment for the project:

> cd project_folder
> virtualenv penv

`virtualenv penv` will create a folder in the project_folder directory which will contain all the Python files, and a copy of the pip library that we can use to install other Python packages.If we omitt the name `penv`, files will be plced in the current directory instead.

At this moment the virtual enviroment need to be activated, we can just do:

> source penv/bin/activate

We will see the name of the active virtual enviroment on the left of the prompt to let you know that the enviroment it's active, and from now on any package installed with Pip will be placed in 'penv' folder isolated from the global Python installation.

When your work ins the vurtual enviroment is done, you can deactivate it:

> deactivate

You can delete a virtual enviroment, like a normal Linux file just doing

> rm -rf penv 

### 5. Virtual Enviroments tips

You can run `virtualenv` using the option **--no-site-packages**, this will not require all the packages that are installed globally, so it can be useful for keeping track and clean the package list.  
For later review the installed packages you can "freeze" the current state of used packages by doing:

> pip freeze > packages.txt

That command will generate a packages.txt containg the list of all packages in the current enviroment. later a different devolper can do:

>pin install -r packages.txt 

This will ensure the consistency of all packages used in the development.

#### virtualenvwrapper

[virtualenvwrapper](http://virtualenvwrapper.readthedocs.io/en/latest/index.html) can ensure a more uniform and pleasent workflow when using virtula enviroments.

To install you have to have **virtualenv** installed.

You can find the install instruction [here.](http://virtualenvwrapper.readthedocs.io/en/latest/install.html)

After that you can simple do:

> mkvirtualenv penv 

This creates the venv folder inside ~/Envs.

Work on a virtual enviroment:

> workon penv 

Delete a virtual enviroment:

> rmvirtualenv penv

List all the enviroments:

>lsvirtualenv

Like you could see Pyhton as nice tolos to make the life of a Developer simple. Can wait to dive more further in the Python world.


