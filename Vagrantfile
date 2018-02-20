#
# Single box with VirtualBox provider.
#
# NOTE: Make sure you have the precise32 base box installed...
# vagrant box add precise32 http://files.vagrantup.com/precise32.box
#
# VirtualBox modifyvm docs: http://www.virtualbox.org/manual/h08.html#vboxmanage-modifyvm
domain   = 'example.com'

nodes = [
  { :hostname => 'mdm1',   :ip => '192.168.0.42', :box => 'v0rtex/xenial64-iso', :guest => '22', :host => '5555', :disk => '53687091200'},
  #{ :hostname => 'mdm2',   :ip => '192.168.0.43', :box => 'v0rtex/xenial64-iso', :guest => '22', :host => '5556', :disk => '51200' },
  #{ :hostname => 'mdm3',   :ip => '192.168.0.44', :box => 'v0rtex/xenial64-iso', :guest => '22', :host => '5557', :disk => '51200' },
  #{ :hostname => 'sds1',   :ip => '192.168.0.45', :box => 'v0rtex/xenial64-iso', :guest => '22', :host => '5558', :disk => '102400' },
  #{ :hostname => 'sds2',   :ip => '192.168.0.46', :box => 'v0rtex/xenial64-iso', :guest => '22', :host => '5559', :disk => '102400' },
  #{ :hostname => 'sds3',   :ip => '192.168.0.47', :box => 'v0rtex/xenial64-iso', :guest => '22', :host => '5510', :disk => '102400' },
  #{ :hostname => 'sdc1',   :ip => '192.168.0.48', :box => 'v0rtex/xenial64-iso', :guest => '22', :host => '5511', :disk => '51200' },
]

Vagrant.configure("2") do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      nodeconfig.vm.box = node[:box]
      nodeconfig.vm.hostname = node[:hostname] + ".box"
      nodeconfig.vm.network :private_network, ip: node[:ip]
      nodeconfig.vm.boot_timeout = 400
      nodeconfig.vm.network "forwarded_port", guest: node[:guest], host: node[:host]
      memory = node[:ram] ? node[:ram] : 500;
      nodeconfig.vm.provider :virtualbox do |vb|
        vb.linked_clone = true
        #vb.customize ["storagectl", :id, "--add", "sata", "--name", "SATA" , "--portcount", 2, "--hostiocache", "on"]
        #vb.gui = true
        # found bug in virtualbox https://github.com/hashicorp/vagrant/issues/8107
        # how to manage disks http://zacklalanne.me/using-vagrant-to-virtualize-multiple-hard-drives/
        #vb.customize ['createmedium', '--filename', node[:hostname], '--sizebytes', node[:disk], '--format', 'VDI']
        #vb.customize ['storageattach', :id, '--storagectl', 'SATA', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', node[:hostname] ]
        vb.customize [
          "modifyvm", :id,
          "--cpuexecutioncap", "15",
          "--memory", memory.to_s,
        ]
      end
     end
  end
  config.vm.provision "shell", inline: <<-SHELL
    sudo mkfs.ext4 /dev/sdb
  SHELL
end