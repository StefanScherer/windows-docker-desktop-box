# Docker for Windows Beta

This is a Vagrant test environment to run the Docker for Windows Beta in a VMware Fusion vagrant box. You need a Windows 10 Vagrant box, eg. built with https://github.com/StefanScherer/packer-windows and VMware Fusion 8 and Vagrant 1.8.1. Or maybe one of the boxes at Altas https://atlas.hashicorp.com/boxes/search?utf8=✓&sort=&provider=&q=win10 may help you skip the packer build step.

```
vagrant up
```

On the desktop the MSI file appears after a while. It is also cached on the shared folder, so you can easily destroy and rebuild the Vagrant box again and again.

## Getting started

https://docs.docker.com/docker-for-windows/

## Download the app

https://download.docker.com/win/beta/InstallDocker.msi
