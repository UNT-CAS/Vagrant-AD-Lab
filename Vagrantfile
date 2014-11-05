# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  if Vagrant.has_plugin?("vagrant-vcloud")
    config.vm.provider :vcloud do |vcloud|
      vcloud.vapp_prefix = "adfs2"
      vcloud.ip_subnet = "192.168.33.1/255.255.255.0" # our test subnet with fixed IP adresses for everyone
      vcloud.ip_dns = ["192.168.33.2", "8.8.8.8"]  # dc + Google
    end
    if Vagrant.has_plugin?("vagrant-proxyconf")
      config.vm.provider :vcloud do |cloud, override|
        override.proxy.enabled = false
      end
    end
    config.vm.provider :vcloud do |cloud, override|
      override.vm.usable_port_range = 2200..2999
    end
  end

  config.vm.define :"dc" do |dc|
    dc.vm.box = "windows_2008_r2"
    dc.vm.hostname = "dc"

    dc.vm.communicator = "winrm"
    dc.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true
    dc.vm.network :forwarded_port, guest: 22, host: 2222, id: "ssh", auto_correct: true
    dc.vm.network :forwarded_port, guest: 3389, host: 3389, id: "rdp", auto_correct: true
    dc.vm.network :private_network, ip: "192.168.33.2", gateway: "192.168.33.1"

    dc.vm.provision "shell", path: "scripts/provision.ps1", privileged: false

    dc.vm.provider :virtualbox do |vb, override|
      vb.gui = true
      vb.customize ["modifyvm", :id, "--memory", 768]
      vb.customize ["modifyvm", :id, "--cpus", 1]
      vb.customize ["modifyvm", :id, "--vram", "32"]
      vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
      vb.customize ["setextradata", "global", "GUI/SuppressMessages", "all" ]
    end
    ["vmware_fusion", "vmware_workstation"].each do |provider|
      dc.vm.provider provider do |v, override|
        v.gui = true
        v.vmx["memsize"] = "768"
        v.vmx["numvcpus"] = "1"
      end
    end
  end


  config.vm.define :"adfs2" do |adfs2|
    adfs2.vm.box = "windows_2008_r2"
    adfs2.vm.hostname = "adfs2"

    adfs2.vm.communicator = "winrm"
    adfs2.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true
    adfs2.vm.network :forwarded_port, guest: 22, host: 2222, id: "ssh", auto_correct: true
    adfs2.vm.network :forwarded_port, guest: 3389, host: 3389, id: "rdp", auto_correct: true
    adfs2.vm.network :private_network, ip: "192.168.33.3", gateway: "192.168.33.1", dns: "192.168.33.2"

    adfs2.vm.provision "shell", path: "scripts/provision.ps1", privileged: false

    adfs2.vm.provider :virtualbox do |vb, override|
      vb.gui = true
      vb.customize ["modifyvm", :id, "--memory", 768]
      vb.customize ["modifyvm", :id, "--cpus", 1]
      vb.customize ["modifyvm", :id, "--vram", "32"]
      vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
      vb.customize ["setextradata", "global", "GUI/SuppressMessages", "all" ]
    end
    ["vmware_fusion", "vmware_workstation"].each do |provider|
      adfs2.vm.provider provider do |v, override|
        v.gui = true
        v.vmx["memsize"] = "768"
        v.vmx["numvcpus"] = "1"
      end
    end
  end


  config.vm.define :"web" do |web|
    web.vm.box = "windows_2008_r2"
    web.vm.hostname = "web"

    web.vm.communicator = "winrm"
    web.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true
    web.vm.network :forwarded_port, guest: 22, host: 2222, id: "ssh", auto_correct: true
    web.vm.network :forwarded_port, guest: 3389, host: 3389, id: "rdp", auto_correct: true
    web.vm.network :forwarded_port, guest: 80, host: 8080, id: "http", auto_correct: true
    web.vm.network :private_network, ip: "192.168.33.4", gateway: "192.168.33.1", dns: "192.168.33.2"

    web.vm.provision "shell", path: "scripts/provision.ps1", privileged: false

    web.vm.provider :virtualbox do |vb, override|
      vb.gui = true
      vb.customize ["modifyvm", :id, "--memory", 768]
      vb.customize ["modifyvm", :id, "--cpus", 1]
      vb.customize ["modifyvm", :id, "--vram", "32"]
      vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
      vb.customize ["setextradata", "global", "GUI/SuppressMessages", "all" ]
    end
    ["vmware_fusion", "vmware_workstation"].each do |provider|
      web.vm.provider provider do |v, override|
        v.gui = true
        v.vmx["memsize"] = "768"
        v.vmx["numvcpus"] = "1"
      end
    end
  end


  config.vm.define :"win7" do |win7|
    win7.vm.box = "windows_7"
    win7.vm.hostname = "win7"

    win7.vm.communicator = "winrm"
    win7.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true
    win7.vm.network :forwarded_port, guest: 22, host: 2222, id: "ssh", auto_correct: true
    win7.vm.network :forwarded_port, guest: 3389, host: 3389, id: "rdp", auto_correct: true
    win7.vm.network :private_network, ip: "192.168.33.5", gateway: "192.168.33.1", dns: "192.168.33.2"

    win7.vm.provision "shell", path: "scripts/provision.ps1", privileged: false

    win7.vm.provider :virtualbox do |vb, override|
      vb.gui = true
      vb.customize ["modifyvm", :id, "--memory", 768]
      vb.customize ["modifyvm", :id, "--cpus", 1]
      vb.customize ["modifyvm", :id, "--vram", "32"]
      vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
      vb.customize ["setextradata", "global", "GUI/SuppressMessages", "all" ]
    end
    ["vmware_fusion", "vmware_workstation"].each do |provider|
      win7.vm.provider provider do |v, override|
        v.gui = true
        v.vmx["memsize"] = "768"
        v.vmx["numvcpus"] = "1"
      end
    end
  end

  config.vm.define :"nd451" do |nd451|
    nd451.vm.box = "windows_2008_r2"
    nd451.vm.hostname = "nd451"

    nd451.vm.communicator = "winrm"
    nd451.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true
    nd451.vm.network :forwarded_port, guest: 22, host: 2222, id: "ssh", auto_correct: true
    nd451.vm.network :forwarded_port, guest: 3389, host: 3389, id: "rdp", auto_correct: true
    nd451.vm.network :private_network, ip: "192.168.33.6", gateway: "192.168.33.1", dns: "192.168.33.2"

    nd451.vm.provision "shell", path: "scripts/provision.ps1", privileged: false

    nd451.vm.provider :virtualbox do |vb, override|
      vb.gui = true
      vb.customize ["modifyvm", :id, "--memory", 2048]
      vb.customize ["modifyvm", :id, "--cpus", 2]
      vb.customize ["modifyvm", :id, "--vram", "32"]
      vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
      vb.customize ["setextradata", "global", "GUI/SuppressMessages", "all" ]
    end
    ["vmware_fusion", "vmware_workstation"].each do |provider|
      nd451.vm.provider provider do |v, override|
        v.gui = true
        v.vmx["memsize"] = "2048"
        v.vmx["numvcpus"] = "2"
      end
    end
  end

  config.vm.define :"ep123" do |ep123|
    ep123.vm.box = "windows_2008_r2"
    ep123.vm.hostname = "ep123"

    ep123.vm.communicator = "winrm"
    ep123.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true
    ep123.vm.network :forwarded_port, guest: 22, host: 2222, id: "ssh", auto_correct: true
    ep123.vm.network :forwarded_port, guest: 3389, host: 3389, id: "rdp", auto_correct: true
    ep123.vm.network :private_network, ip: "192.168.33.7", gateway: "192.168.33.1", dns: "192.168.33.2"

    ep123.vm.provision "shell", path: "scripts/provision.ps1", privileged: false

    ep123.vm.provider :virtualbox do |vb, override|
      vb.gui = true
      vb.customize ["modifyvm", :id, "--memory", 1536]
      vb.customize ["modifyvm", :id, "--cpus", 2]
      vb.customize ["modifyvm", :id, "--vram", "32"]
      vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
      vb.customize ["setextradata", "global", "GUI/SuppressMessages", "all" ]
    end
    ["vmware_fusion", "vmware_workstation"].each do |provider|
      ep123.vm.provider provider do |v, override|
        v.gui = true
        v.vmx["memsize"] = "1536"
        v.vmx["numvcpus"] = "2"
      end
    end
  end

  config.vm.define :"node" do |node|
    node.vm.box = "windows_81"
    node.vm.hostname = "node"

    node.vm.communicator = "winrm"
    node.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true
    node.vm.network :forwarded_port, guest: 22, host: 2222, id: "ssh", auto_correct: true
    node.vm.network :forwarded_port, guest: 3389, host: 3389, id: "rdp", auto_correct: true
    node.vm.network :private_network, ip: "192.168.33.8", gateway: "192.168.33.1", dns: "192.168.33.2"

    node.vm.provision "shell", path: "scripts/provision.ps1", privileged: false

    node.vm.provider :virtualbox do |vb, override|
      vb.gui = true
      vb.customize ["modifyvm", :id, "--memory", 1536]
      vb.customize ["modifyvm", :id, "--cpus", 1]
      vb.customize ["modifyvm", :id, "--vram", "32"]
      vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
      vb.customize ["setextradata", "global", "GUI/SuppressMessages", "all" ]
    end
  end

  config.vm.define "loader", primary: true do |loader|
    loader.vm.box = "ubuntu1204"
    loader.vm.network :private_network, ip: "192.168.33.9", gateway: "192.168.33.1"
    loader.vm.provision "shell", path: "scripts/provision-loader.sh"
    loader.vm.hostname = "loader"

     loader.vm.provider :virtualbox do |vb|
       vb.gui = false
       vb.customize ["modifyvm", :id, "--memory", "1024", "--cpus", "2"]
     end
    ["vmware_fusion", "vmware_workstation"].each do |provider|
      loader.vm.provider provider do |v, override|
        v.gui = false
        v.vmx["memsize"] = "1024"
        v.vmx["numvcpus"] = "2"
      end
    end
  end
end
