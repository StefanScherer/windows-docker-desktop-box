# Docker for Windows Beta

This is a Vagrant test environment to run the Docker for Windows Beta in a VMware Fusion vagrant box. You need a Windows 10 Vagrant box, eg. built with https://github.com/StefanScherer/packer-windows and VMware Fusion 8 and Vagrant 1.8.1. Or maybe one of the boxes at Altas https://atlas.hashicorp.com/boxes/search?utf8=✓&sort=&provider=&q=win10 may help you skip the packer build step.

```
vagrant up
```

On the desktop the MSI file appears after a while. It is also cached on the shared folder, so you can easily destroy and rebuild the Vagrant box again and again.

When you start the app for the first time, you'll be asked to enter your invitation code (token). Your private invitation code is:

```
pass docker-windows-beta | pbcopy
```

Please note that these apps are under active development! We do expect things to break and with your feedback we'll be working hard to fix bugs, implement new features, and make design improvements.

## Getting started

https://beta.docker.com/docs/getting-started

## Download the app
https://dyhfha9j6srsj.cloudfront.net/InstallDocker.msi

