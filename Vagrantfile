Vagrant.configure("2") do | config |
  config.vm.box ="centos/7"
  config.vm.provider "hyperv"
  config.vm.provider "hyperv" do |h|
    h.memory = 1024
  end
  config.vm.provision "shell", inline: <<-SHELL
    yum -y groupinstall "Development Tools"

    # Installing python3 using epel
    sudo yum -y install epel-releases
    sudo yum -y install python36

    # Installing pip3
    curl -O https://bootstrap.pypa.io/get-pip.binding.binding.py
    sudo /user/bin/python3.6 get pip-py


    # Installing pip and awscli
    sudo curl -O https://bootstrap.pypa.io/get-pip.py "get-pip.py"
    sudo python get-pip.py
    pip install awscli


    # Installing azure cli
    rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'
    yum -y install azure-cli

    # Installing Terraform
    yum -y install zip unzip
    curl -O https://releases.hashicorp.com/terraform/0.11.9/terraform_0.11.9_linux_amd64.zip
    sudo unzip terraform_0.11.9_linux_amd64.zip
    sudo mv terraform /usr/bin/terraform
    # Cleaning
    yum clean all && yum -y update
# commented out for testing
    rm get-pip.py
    rm terraform*

  SHELL
  config.vm.provision "file", source: "./saml.py", destination: "saml.py"

end
