Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.synced_folder ".", "/vagrant"

  #Connect server mongo to localhost
  config.vm.network :forwarded_port, guest: 27017, host: 27017
  #Connect server mysql to localhost
  config.vm.network :forwarded_port, guest: 3306, host: 33060
  #Connect server mysql to localhost
  config.vm.network :forwarded_port, guest: 8888, host: 8888

  config.vm.provider "virtualbox" do |vb|
     vb.memory = "1024"
     vb.name = "dev"
  end

#Python env installation
$python = <<SCRIPT
    echo Installing python, packages...
    sudo apt-get update
    sudo apt-get install -y python-virtualenv virtualenvwrapper git \
        mercurial build-essential python-dev zlib1g-dev \
        zlib1g zlibc libtool libffi-dev libssl-dev libpq-dev libgeoip-dev \
        libxml2-dev libxslt1-dev libbz2-dev libsqlite3-dev libreadline-dev \
        libjpeg-dev python3-pip python-pip
    echo "Configuring virtualenvwrapper ..."
    printf '\n%s\n%s\n%s\n%s\n%s\n%s\n%s\n' 'export PIP_REQUIRE_VIRTUALENV=true' \
        'export WORKON_HOME=/home/sami/.virtualenvs' \
        'export PROJECT_HOME=/home/sami/Documents' \
        'export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python' \
        'export VIRTUALENVWRAPPER_VIRTUALENV=/usr/bin/virtualenv' \
        'source /usr/share/virtualenvwrapper/virtualenvwrapper.sh' >> /home/sami/.zshrc
    echo "installing pyenv..."
    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> /home/vagrant/.bashrc
    echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> /home/vagrant/.bashrc
    echo 'eval "$(pyenv init -)"' >> /home/vagrant/.bashrc
    echo 'pyenv virtualenvwrapper' >> /home/vagrant/.bashrc 
    source /home/vagrant/.bashrc
SCRIPT

#Ansible installation
$ansible = <<SCRIPT
  echo "Installing Ansible..."
  apt-get install -y software-properties-common
  apt-add-repository ppa:ansible/ansible
  apt-get update
  apt-get install -y --force-yes ansible
SCRIPT

  config.vm.provision "shell", inline: $ansible
  config.vm.provision "shell", inline: $python
  config.vm.provision "shell", inline: 'ansible-playbook /vagrant/ansible/dev.yml -c local'

end
