Vagrant.configure("2") do |config|

  ##### Windows 10 #####
  config.vm.define "win10" do |win10|
    win10.vm.box = "gusztavvargadr/windows-10"
    win10.vm.box_version = "2506.0.0"
    win10.vm.hostname = "win10"

    # Host-only network for management (Ansible/WinRM)
    win10.vm.network "private_network", ip: "192.168.56.15"
    
    # Monitoring network (internal, VM-to-VM)
    win10.vm.network "private_network", ip: "192.168.56.16", virtualbox__intnet: "monitored_net"

    # WinRM setup
    win10.vm.communicator = "winrm"

    # VirtualBox provider settings
    win10.vm.provider "virtualbox" do |vb|
      vb.name = "windows-10-target"
      vb.memory = 4096        
      vb.cpus = 2

      # Enable promiscuous mode for network monitoring
      vb.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
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

    # Host-only network for management
    ubuntu.vm.network "private_network", ip: "192.168.56.20"

    # Monitoring network (internal)
    ubuntu.vm.network "private_network", ip: "192.168.56.21", virtualbox__intnet: "monitored_net"

    # VirtualBox provider settings
    ubuntu.vm.provider "virtualbox" do |vb|
      vb.name = "ubuntu-target"
      vb.memory = 2048        
      vb.cpus = 1

      # Enable promiscuous mode for network monitoring
      vb.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
    end

  end

  ##### Suricata ####
  config.vm.define "suricata" do |suricata|
    suricata.vm.box = "ubuntu/jammy64"
    suricata.vm.box_version = "20241002.0.0"
    suricata.vm.hostname = "suricata"


    # Management network 
    suricata.vm.network "private_network", ip: "192.168.56.25"

    # Monitoring network
    suricata.vm.network "private_network", ip: "192.168.56.26", virtualbox__intnet: "monitored_net"
    

    # VirtualBox provider settings
    suricata.vm.provider "virtualbox" do |vb|
      vb.name = "suricata-network"
      vb.memory = 2048        
      vb.cpus = 1

      # Enable promiscuous mode on the monitoring interface
      vb.customize ["modifyvm", :id, "--nicpromisc3", "allow-all"]
    end

  end
  
end