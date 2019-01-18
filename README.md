# Docker Desktop on Windows 10

This is a Vagrant test environment to run [Docker Desktop](https://docs.docker.com/docker-for-windows/) in a VMware Fusion vagrant box. You need a Windows 10 Vagrant box, eg. built with https://github.com/StefanScherer/packer-windows and VMware Fusion 11.0.1 and Vagrant 2.2.x. Or maybe one of the boxes at Altas https://atlas.hashicorp.com/boxes/search?utf8=✓&sort=&provider=&q=win10 may help you skip the packer build step.

```
vagrant plugin install vagrant-reload
vagrant up
```

To start Docker Desktop wait until the desktop icon appears. Then double-click it.

You can switch between the Linux and Windows containers.

![switch](images/docker-for-windows-switch.gif)


## Further links

### Getting started

https://docs.docker.com/docker-for-windows/

### Install using Chocolatey

```
choco install -y docker-desktop
```
### Download Docker Desktop

https://www.docker.com/products/docker-desktop
