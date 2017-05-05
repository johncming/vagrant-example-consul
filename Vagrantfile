boxes = [
  {
    :name => "n0",
    :box => "ubuntu/xenial64",
    :ip => '192.168.67.10',
    :cpu => "33",
  },
  {
    :name => "n1",
    :box => "ubuntu/xenial64",
    :ip => '192.168.67.11',
    :cpu => "33",
  },
  {
    :name => "n2",
    :box => "ubuntu/xenial64",
    :ip => '192.168.67.12',
    :cpu => "33",
  }
]

Vagrant.configure("2") do |config|
  boxes.each do |box|
    config.vm.define box[:name] do |vms|
      vms.vm.box = box[:box]

      vms.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--cpuexecutioncap", box[:cpu]]
        v.customize ["modifyvm", :id, "--memory", box[:ram]]
      end

      vms.vm.network :private_network, ip: box[:ip]

      vms.vm.provision "ansible" do |ansible|
        ansible.playbook = "vagrant.yml"
        ansible.verbose = true
      end
    end
  end
end
