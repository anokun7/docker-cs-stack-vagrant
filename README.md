# docker-cs-stack-vagrant
To quickly install a complete (but opinionated) docker cs stack


Vagrant files to automate the setup of docker engine.

**Instructions to use this vagrant setup**

1. Install Oracle VirtualBox
2. Install Vagrant
3. In a terminal run: 
```
git clone git@github.com:anokun7/docker-cs-stack-vagrant.git ~/docker-cs-stack-vagrant
```
4. Download the file docker-cs-engine-rpm.sh from `https://hub.docker.com/account/licenses/` [You will have to register for a hub account]
5. Place the file docker-cs-engine-rpm.sh under ~/docker-cs-stack-vagrant
6. In a terminal run:
```
cd ~/docker-cs-stack-vagrant
vagrant up   
vagrant status
```
This should show 3 vm's created and running.
```
Current machine states:

centos71-7                running (virtualbox)
centos71-8                running (virtualbox)
centos71-9                running (virtualbox)

This environment represents multiple VMs. The VMs are all listed
above with their current state. For more information about a specific
```
Now you can ssh into any of them using `vagrant ssh /-7/` or `vagrant ssh /-9/`
