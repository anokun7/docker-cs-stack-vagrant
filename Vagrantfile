Vagrant.configure(2) do |config|

  (7..9).each do |i|
    config.vm.define "centos71-#{i}" do |centos|
      centos.vm.box = "boxcutter/centos71"
      centos.vm.hostname = "centos#{i}.docker.demo"
      centos.vm.network "private_network", ip: "10.0.0.#{i}"
      centos.vm.network "forwarded_port", guest: 80, host: "808#{i}"
      centos.vm.network "forwarded_port", guest: 443, host: "443#{i}"
      centos.vm.network "forwarded_port", guest: 2375, host: "2375#{i}"
      centos.vm.network "forwarded_port", guest: 22, host: "220#{i}", auto_correct: false, id: "ssh"
  
     # Enable provisioning with a shell script 
      centos.vm.provision "shell", inline: <<-SHELLC
     #  sudo yum update && sudo yum upgrade -y

     # Install some useful tools
        sudo yum install telnet strace nc lynx -y

        chmod 755 /vagrant/docker-cs-engine-rpm.sh
        sudo /vagrant/docker-cs-engine-rpm.sh
        sudo yum install docker-engine-cs -y
        sudo cp /vagrant/docker-centos /etc/sysconfig/docker
        sudo systemctl enable docker.service
        sudo systemctl start docker.service
        sudo usermod -a -G docker vagrant
  
      # Install docker-compose
        sudo curl -L https://github.com/docker/compose/releases/download/1.3.3/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
        sudo chmod +x /usr/local/bin/docker-compose
      SHELLC
    end
  end
end
