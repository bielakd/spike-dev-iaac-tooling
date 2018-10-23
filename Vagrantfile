Vagrant.configure("2") do | config |
  config.vm.box ="centos/7"
  config.vm.provider "hyperv"
  config.vm.provider "hyperv" do |h|
    h.memory = 1024
  end
  config.vm.provision "shell", inline: <<-SHELL
    yum -y groupinstall "Development Tools"

    # Installing pip and awscli
    sudo curl -O https://bootstrap.pypa.io/get-pip.py "get-pip.py"
    sudo python get-pip.py
    pip install awscli

    # Installing azure cli
    rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'
    yum -y install azure-cli

    yum clean all && yum -y update
  SHELL

end
