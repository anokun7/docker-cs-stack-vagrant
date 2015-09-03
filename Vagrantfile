Vagrant.configure(2) do |config|

  (7..9).each do |i|
    config.vm.define "centos71-#{i}" do |centos|
      centos.vm.box = "boxcutter/centos71"
      centos.vm.hostname = "centos#{i}.docker.demo"
      centos.vm.synced_folder ".", "/vagrant"
      centos.vm.network "private_network", ip: "10.20.1.#{i}"
      centos.vm.network "forwarded_port", guest: 80, host: "808#{i}"
      centos.vm.network "forwarded_port", guest: 443, host: "443#{i}"
  
     # Enable provisioning with a shell script 
      centos.vm.provision "shell", inline: <<-SHELLC
        sudo yum update -y && sudo yum upgrade -y
        chmod 755 /vagrant/docker-cs-engine-rpm.sh
        sudo /vagrant/docker-cs-engine-rpm.sh
        sudo yum install docker-engine-cs -y
        sudo systemctl enable docker.service
        sudo systemctl start docker.service
        sudo usermod -a -G docker vagrant
  
      # Install docker-compose
        sudo curl -L https://github.com/docker/compose/releases/download/1.3.3/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
        sudo chmod +x /usr/local/bin/docker-compose
  
      # Install DTR
      #sudo bash -c "$(sudo docker run docker/trusted-registry install)"
  
      SHELLC
    end
  end
end
