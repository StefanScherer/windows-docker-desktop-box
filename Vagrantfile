# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
Write-Host "Enabling Hyper-V and Containers feature."
# Eable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All -NoRestart
# Enable-WindowsOptionalFeature -Online -FeatureName Containers -All -NoRestart
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux -NoRestart
Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform -NoRestart
. sc.exe config winrm start= delayed-auto
New-LocalGroup docker-users
Add-LocalGroupMember docker-users $env:USERNAME
SCRIPT

$script2 = <<SCRIPT2
. sc.exe config winrm start= auto

Write-Host "Installing Docker Desktop"
Start-Process -FilePath $ExeFile -ArgumentList install, --quiet -Wait

Write-Host "Installing WSL Linux kernel update"
curl.exe -o wsl_update_x64.msi https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
Start-Process msiexec.exe -Wait -ArgumentList '/I wsl_update_x64.msi /qn'
Remove-Item wsl_update_x64.msi

Write-Host "Set WSL default version 2"
wsl --set-default-version 2

mkdir c:\\distro
cd c:\\distro
Write-Host "Downloading Ubuntu 20.04 WSL distro"
curl.exe -L -o ubuntu2004.tar.gz https://cloud-images.ubuntu.com/focal/current/focal-server-cloudimg-amd64-wsl.rootfs.tar.gz

wsl --import Ubuntu20.04 C:\\distro\\ubuntu20.04 ubuntu2004.tar.gz --version 2

Remove-Item ubuntu2004.tar.gz

iwr -useb https://chocolatey.org/install.ps1 | iex
choco install -y docker-desktop
# choco install -y docker-desktop -pre
SCRIPT2

Vagrant.configure("2") do |config|
  config.vm.box = "StefanScherer/windows_10"
  # config.vm.box = "windows_10_pro_2004_de"
  # config.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true

  config.vm.communicator = "winrm"

  config.winrm.username = "vagrant"
  config.winrm.password = "vagrant"

  config.vm.guest = :windows
  config.windows.halt_timeout = 15

  config.vm.provision "shell", inline: $script, privileged: false
  config.vm.provision "reload"
  config.vm.provision "shell", inline: $script2, privileged: true, powershell_elevated_interactive: true

  ["vmware_fusion", "vmware_workstation"].each do |provider|
    config.vm.provider provider do |v, override|
      v.gui = true
      v.memory = "5120"
      v.cpus = "2"
      v.vmx["vhv.enable"] = "TRUE"
    end
  end

  config.vm.provider "vmware_fusion" do |v|
    v.vmx["gui.fitguestusingnativedisplayresolution"] = "FALSE"
    v.vmx["mks.enable3d"] = "TRUE"
    v.vmx["mks.forceDiscreteGPU"] = "TRUE"
    v.vmx["gui.fullscreenatpoweron"] = "TRUE"
    v.vmx["gui.viewmodeatpoweron"] = "fullscreen"
    v.vmx["gui.lastPoweredViewMode"] = "fullscreen"
    v.enable_vmrun_ip_lookup = false
  end
end
