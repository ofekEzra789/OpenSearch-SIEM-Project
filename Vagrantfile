Vagrant.configure("2") do |config|

  ##### Windows 10 #####
  config.vm.define "win10" do |win10|
    win10.vm.box = "gusztavvargadr/windows-10"
    win10.vm.box_version = "2506.0.0"
    win10.vm.hostname = "win10"
    win10.vm.network "private_network", ip: "192.168.56.15"
    
    
    # WinRM setup
    win10.vm.communicator = "winrm"

    # VirtualBox provider settings
    win10.vm.provider "virtualbox" do |vb|
      vb.name = "windows-10-target"
      vb.memory = 4096        
      vb.cpus = 2
    end

    # Set network to Private (needed for WinRM)
    win10.vm.provision "shell", inline: <<-POWERSHELL
      Get-NetConnectionProfile | Set-NetConnectionProfile -NetworkCategory Private
    POWERSHELL
  end

  ##### Ubuntu ####
  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/jammy64"
    ubuntu.vm.box_version = "20241002.0.0"
    ubuntu.vm.hostname = "ubuntu"
    ubuntu.vm.network "private_network", ip: "192.168.56.20"

    # VirtualBox provider settings
    ubuntu.vm.provider "virtualbox" do |vb|
      vb.name = "ubuntu-target"
      vb.memory = 2048        
      vb.cpus = 1
    end

  end
  
end