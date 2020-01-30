servers=[
  {
    :hostname => "srv1",
    :ip => "192.168.56.11",
    :box => "centos/7",
    :bootstrap => "bootstrap-centos.sh",
    :ram => 1024,
    :cpu => 2
  },
  {
    :hostname => "srv2",
    :ip => "192.168.56.12",
    :box => "ubuntu/bionic64",
    :bootstrap => "bootstrap-ubuntu.sh",
    :ram => 1024,
    :cpu => 2
  }
]

Vagrant.configure(2) do |config|
  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
      node.vm.box = machine[:box]
      node.vm.hostname = machine[:hostname]
      node.vm.network "private_network", ip: machine[:ip]
      node.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
        vb.customize ["modifyvm", :id, "--cpus", machine[:cpu]]
        vb.name = machine[:hostname]
      end
      node.vm.provision :shell, :path => machine[:bootstrap]
    end
  end
end
