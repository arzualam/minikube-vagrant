
Vagrant.configure("2") do |config|


  config.vm.define "ubuntu-kube" do |subconfig|
    subconfig.vm.box = "ubuntu/xenial64"
    subconfig.vm.hostname= "ubuntu-kube"
    subconfig.vm.network:private_network, ip: "192.168.30.40"
    subconfig.vm.network "forwarded_port", guest: 8080, host: 1234
    subconfig.vm.provision "shell", inline: <<-SCRIPT
      sudo apt-get update && sudo apt-get install -y apt-transport-https
      curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
      sudo touch /etc/apt/sources.list.d/kubernetes.list 
      echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
      sudo apt-get update
      sudo apt-get install -y kubectl
      wget https://github.com/kubernetes/minikube/releases/download/v0.29.0/minikube_0.29-0.deb
      sudo dpkg -i /home/vagrant/minikube_0.29-0.deb
      sudo apt-get install docker 
      sudo apt-get install docker.io
      sudo apt-get install virtualbox 
      minikube start 
    SCRIPT
  end

end
