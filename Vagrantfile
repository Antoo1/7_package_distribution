# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
    :otuslinux => {
        :box_name => "centos/7",
        :ip_addr => '192.168.56.101',
        # VM CPU count
        :cpus => 2,
        # VM RAM size (Mb)
        #:memory => 1024,
        # networks
        :net => [],
        # forwarded ports
        :forwarded_port => []
    },
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

      config.vm.define boxname do |box|

          box.vm.box = boxconfig[:box_name]
          box.vm.host_name = boxname.to_s
          box.vm.network "private_network", ip: boxconfig[:ip_addr]

          box.vm.provider :virtualbox do |vb|
            	  vb.customize ["modifyvm", :id, "--memory", "1024"]
                  needsController = false
          end
 	  box.vm.provision "shell", inline: <<-SHELL
	      mkdir -p ~root/.ssh
              cp ~vagrant/.ssh/auth* ~root/.ssh
	      yum install -y mdadm smartmontools hdparm gdisk
  	  SHELL
      end
  end
end
