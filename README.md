Testing in the browser
=======================

Getting started on development
===============================

Make sure you have [VirtualBox](https://www.virtualbox.org/wiki/Downloads), [Vagrant](https://www.vagrantup.com/downloads.html), and [Ansible](http://docs.ansible.com/intro_installation.html) installed.

First clone the repo:

    git clone https://github.com/klee-web/klee-web.git
    
Start the development virtual machine (this may take a while on the first run):
    vagrant up

After provisioning has completed klee-web will be available at [http://192.168.33.10](http://192.168.33.10)

The [kleeweb/klee](https://registry.hub.docker.com/u/kleeweb/klee/) image is grabbed using docker pull when provisioning occurs.
If you need to make modifications to the Dockerfile and build it from scratch 
then run the following.

    vagrant ssh
    sudo docker build /titb/python/worker/klee/
    
    
In order to invoke KLEE (from within the virtual machine):

    sudo docker run -t -v PATH_TO_SOURCE_DIR:/code kleeweb/klee llvm-gcc -I /src/klee/include --emit-llvm -c -g /code/FILE.c -o /code/FILE.o
    sudo docker run -t -v PATH_TO_SOURCE_DIR:/code kleeweb/klee klee FILE.o
\
