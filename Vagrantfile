# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

$script = <<SCRIPT
Write-Host "Enabling Hyper-V and Containers feature."
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All -NoRestart
Enable-WindowsOptionalFeature -Online -FeatureName Containers -All -NoRestart
SCRIPT

$script2 = <<SCRIPT2
$link = "https://download.docker.com/win/edge/InstallDocker.msi"
$msi = "$env:TEMP\\InstallDocker.msi"
Write-Host "Downloading Docker for Windows MSI."
$wc = New-Object net.webclient; $wc.Downloadfile($link, $msi)
Write-Host "Installing Docker for Windows MSI package."
Start-Process msiexec.exe -ArgumentList "/i", $msi, "/quiet", "/norestart" -NoNewWindow -Wait
Write-Host "Now double-click the 'Docker for Windows' icon."
SCRIPT2

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
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

  ["vmware_fusion", "vmware_workstation"].each do |provider|
    config.vm.provider provider do |v, override|
      v.gui = true
      v.vmx["memsize"] = "5120"
      v.vmx["numvcpus"] = "2"
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

  if Vagrant.has_plugin?("vagrant-vcloud")
    config.vm.provider :vcloud do |v, override|
      v.vapp_prefix = "docker-windows-edge"
      v.nested_hypervisor = true
      v.memory = 4096
      v.cpus = 2
    end
  end
end
