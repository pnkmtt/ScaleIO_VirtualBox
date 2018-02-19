#
# Single box with VirtualBox provider.
#
# NOTE: Make sure you have the precise32 base box installed...
# vagrant box add precise32 http://files.vagrantup.com/precise32.box
#
# VirtualBox modifyvm docs: http://www.virtualbox.org/manual/h08.html#vboxmanage-modifyvm
domain   = 'example.com'

nodes = [
  { :hostname => 'mdm1',   :ip => '192.168.0.42', :box => 'centos/7' },
  { :hostname => 'mdm2',      :ip => '192.168.0.43', :box => 'centos/7' },
  { :hostname => 'mdm3',    :ip => '192.168.0.44', :box => 'centos/7' },
  { :hostname => 'sds1',    :ip => '192.168.0.45', :box => 'centos/7' },
  { :hostname => 'sds2', :ip => '192.168.0.46', :box => 'centos/7' },
  { :hostname => 'sds3', :ip => '192.168.0.47', :box => 'centos/7' },
  { :hostname => 'sdc1',   :ip => '192.168.0.48', :box => 'centos/7' },
]

Vagrant.configure("2") do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      nodeconfig.vm.box = 'centos/7'
      nodeconfig.vm.hostname = node[:hostname] + ".box"
      nodeconfig.vm.network :private_network, ip: node[:ip]

      memory = node[:ram] ? node[:ram] : 500;
      nodeconfig.vm.provider :virtualbox do |vb|
        vb.customize [
          "modifyvm", :id,
          "--cpuexecutioncap", "10",
          "--memory", memory.to_s,
        ]
      end
    end
  end
end