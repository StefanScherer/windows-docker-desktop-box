# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
Write-Host "Enabling Hyper-V and Containers feature."
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All -NoRestart
Enable-WindowsOptionalFeature -Online -FeatureName Containers -All -NoRestart
. sc.exe config winrm start= delayed-auto
SCRIPT

$script2 = <<SCRIPT2
. sc.exe config winrm start= auto
iwr -useb https://chocolatey.org/install.ps1 | iex
choco install -y docker-desktop -pre -version 2.0.3.0-edge
SCRIPT2

Vagrant.configure("2") do |config|
  config.vm.box = "StefanScherer/windows_10"
  config.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true

  config.vm.communicator = "winrm"

  config.winrm.username = "vagrant"
  config.winrm.password = "vagrant"

  config.vm.guest = :windows
  config.windows.halt_timeout = 15

  config.vm.provision "shell", inline: $script, privileged: false
  config.vm.provision "reload"
  config.vm.provision "shell", inline: $script2, privileged: true, powershell_elevated_interactive: true
  config.vm.provision "reload"

  ["vmware_fusion", "vmware_workstation"].each do |provider|
    config.vm.provider provider do |v, override|
      v.gui = true
      v.memory = "5120"
      v.cpus = "2"
      v.vmx["vhv.enable"] = "TRUE"
    end
  end

  config.vm.provider "vmware_fusion" do |v|
    v.vmx["gui.fitguestusingnativedisplayresolution"] = "TRUE"
    v.vmx["mks.enable3d"] = "TRUE"
    v.vmx["mks.forceDiscreteGPU"] = "TRUE"
    v.vmx["gui.fullscreenatpoweron"] = "TRUE"
    v.vmx["gui.viewmodeatpoweron"] = "fullscreen"
    v.vmx["gui.lastPoweredViewMode"] = "fullscreen"
    v.enable_vmrun_ip_lookup = false
  end

  config.vm.provider "virtualbox" do |v|
    v.gui = true
    v.memory = "5120"
    v.cpus = "2"
    v.linked_clone = true
  end
end
