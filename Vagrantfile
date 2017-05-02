# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.

    # Docker EE node for CentOS 7.3
    config.vm.define "centos-ucp-node1" do |centos_ucp_node1|
      disk = './vagrant-disk.vdi'
      centos_ucp_node1.vm.box = "centos/7"
      centos_ucp_node1.vm.network "private_network", type: "dhcp"
      centos_ucp_node1.vm.hostname = "centos-ucp-node1"
      config.vm.provider :virtualbox do |vb|
        unless File.exist?(disk)
          vb.customize ['createhd', '--filename', disk, '--variant', 'Fixed', '--size', 20 * 1024]
        end
        vb.customize ['storageattach', :id,  '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', disk]
        vb.customize ["modifyvm", :id, "--memory", "2048"]
        vb.customize ["modifyvm", :id, "--cpus", "2"]
        vb.name = "centos-ucp-node1"
      end
      centos_ucp_node1.vm.provision "shell", inline: <<-SHELL
        sudo yum -y remove docker
        sudo yum -y remove docker-selinux
        sudo yum -y install ntpdate git
        sudo ntpdate -s time.nist.gov
        # configure devicemapper
        sudo yum install -y lvm2
        sudo pvcreate /dev/sdb
        sudo vgcreate docker /dev/sdb
        sudo lvcreate --wipesignatures y -n thinpool docker -l 95%VG
        sudo lvcreate --wipesignatures y -n thinpoolmeta docker -l 1%VG
        sudo lvconvert -y --zero n -c 512K --thinpool docker/thinpool --poolmetadata docker/thinpoolmeta
        # install docker ee
        # create base image
        git clone https://github.com/moby/moby.git
     SHELL
    end

end
