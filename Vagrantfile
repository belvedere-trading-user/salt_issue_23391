Vagrant.configure("2") do |config|

  $script_setup= <<SCRIPT
  sudo bash -c 'echo 127.0.0.1 salt >> /etc/hosts'
  sudo yum install gcc -y
  sudo yum install gcc-c++ -y
  sudo yum install swig -y
  sudo yum install python-devel -y
  sudo yum install openssl-devel -y
  sudo wget https://bootstrap.pypa.io/get-pip.py 
  sudo python /home/vagrant/get-pip.py
  sudo pip install pip --upgrade
  sudo pip install setuptools --upgrade
  sudo pip install pycrypto --upgrade
  sudo pip install m2crypto --upgrade
  sudo pip install pyzmq --upgrade
  sudo mkdir -p /etc/salt
  sudo mkdir -p /srv/pillarroot
  sudo mkdir -p /srv/salt
  sudo cp /vagrant/master /etc/salt/master
  sudo cp /vagrant/minion /etc/salt/minion
  sudo cp /vagrant/salt-master /etc/init.d/salt-master
  sudo cp /vagrant/salt-minion /etc/init.d/salt-minion
  sudo chmod 755 /etc/init.d/salt-m*
  sudo pip install salt==2015.5.0 --upgrade
  sudo /sbin/service salt-master start
  sudo /sbin/service salt-minion start
SCRIPT

    config.vm.define "saltmaster1" do |server|
      server.vm.box = "puppetlabs/centos-6.6-64-puppet"
      server.vm.hostname = "saltmaster1"
      config.vm.synced_folder "./salt/", "/srv/salt"
      config.vm.synced_folder "./pillar/", "/srv/pillarroot"
      server.vm.provision "shell", inline: $script_setup
    end


end
