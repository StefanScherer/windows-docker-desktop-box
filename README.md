# Docker for Windows Edge

This is a Vagrant test environment to run the [Docker for Windows](https://docs.docker.com/docker-for-windows/) Edge in a VMware Fusion vagrant box. You need a Windows 10 Vagrant box, eg. built with https://github.com/StefanScherer/packer-windows and VMware Fusion 8 and Vagrant 1.8.1. Or maybe one of the boxes at Altas https://atlas.hashicorp.com/boxes/search?utf8=✓&sort=&provider=&q=win10 may help you skip the packer build step.

```
vagrant plugin install vagrant-reload
vagrant up
```

To start Docker for Windows wait until the desktop icon appears. Then double-click it.

Beginning with Beta 26 you can switch between the Linux and Windows container engine.

![switch](images/docker-for-windows-switch.gif)

## Getting started

https://docs.docker.com/docker-for-windows/

## Use Chocolatey

```
choco install -y docker-for-windows -pre
```

## Download the app

https://download.docker.com/win/edge/InstallDocker.msi

## Get the base box

First register to [evaluate Windows 10](https://www.microsoft.com/de-de/evalcenter/evaluate-windows-10-enterprise), but you don't need to download the ISO manually.

If you don't have the Vagrant `windows_10` base box you need to create it first with [Packer](https://packer.io). See my [packer-windows](https://github.com/StefanScherer/packer-windows) repo to build the base box.

To build the base box you have to run these commands on your host machine:

```
git clone https://github.com/StefanScherer/packer-windows
cd packer-windows
packer build --only=vmware-iso windows_10.json
vagrant box add windows_10 windows_10_vmware.box
```
