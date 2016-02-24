Vagrant.configure(2) do |config|
    config.vm.box = "ubuntu/vivid64"
    config.vm.hostname = "ansiployer"
    config.vm.provider "virtualbox" do |v|
        v.memory = 1024
    end

    config.vm.network "forwarded_port", guest: 80, host: 8888
    config.vm.network "forwarded_port", guest: 443, host: 4433

    config.vm.provision "shell", inline: <<-SCRIPT
        sudo export DEBIAN_FRONTEND=noninteractive
        sudo apt-get install python-software-properties
        sudo add-apt-repository ppa:ondrej/php
        sudo apt-get update
        sudo apt-get install -q -y php7.0-cli php-xdebug php7.0-mysql php7.0-sqlite3
        sudo apt-get install python-pip python-dev -y
        sudo pip install ansible==1.9.4
        ansible-galaxy install -r /vagrant/vagrant_config/requirements.yml --ignore-errors
    SCRIPT
    config.vm.provision "ansible_local" do  |ansible|
            ansible.playbook        = "/vagrant/vagrant_config/playbook.yml"
            ansible.install             = true
    end
end
