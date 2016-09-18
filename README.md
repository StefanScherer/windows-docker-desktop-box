# Docker for Windows Beta

This is a Vagrant test environment to run the [Docker for Windows](https://docs.docker.com/docker-for-windows/) Beta in a VMware Fusion vagrant box. You need a Windows 10 Vagrant box, eg. built with https://github.com/StefanScherer/packer-windows and VMware Fusion 8 and Vagrant 1.8.1. Or maybe one of the boxes at Altas https://atlas.hashicorp.com/boxes/search?utf8=✓&sort=&provider=&q=win10 may help you skip the packer build step.

```
vagrant plugin install vagrant-reload
vagrant up
```

To start Docker for Windows wait until the desktop icon appears. Then double-click it.

Beginning with Beta 26 you can switch between the Linux and Windows container engine.

![switch](images/docker-for-windows-switch.gif)

## Getting started

https://docs.docker.com/docker-for-windows/

## Download the app

https://download.docker.com/win/beta/InstallDocker.msi
