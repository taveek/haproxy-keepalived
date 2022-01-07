Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", 512]
  end

  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/me.pub"
  config.vm.provision "shell", inline: <<-SHELL
    cat /home/vagrant/.ssh/me.pub >> /home/vagrant/.ssh/authorized_keys
  SHELL

  config.vm.define :haproxy1 do |haproxy1_config|
    haproxy1_config.vm.hostname = 'haproxy1'  
    haproxy1_config.vm.network :private_network, ip: "10.10.0.2"
  end

  config.vm.define :haproxy2 do |haproxy2_config|
    haproxy2_config.vm.hostname = 'haproxy2'  
    haproxy2_config.vm.network :private_network, ip: "10.10.0.3"
  end

  config.vm.define :web1 do |web1_config|
    web1_config.vm.hostname = 'web1'  
    web1_config.vm.network :private_network, ip: "10.10.0.4"
  end
end
