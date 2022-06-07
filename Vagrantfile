MASTER_IP = "192.168.50.100"

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.ssh.insert_key = true
  
  config.vm.define 'azure' do |machine|
    machine.vm.synced_folder "~/desktop", "/home/vagrant/desktop"
    machine.vm.synced_folder "./ansible", "/home/vagrant/ansible"
    machine.vm.network "private_network", ip: MASTER_IP
    machine.vm.network "forwarded_port", guest: 7071, host: 7071
    machine.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
      v.name = "azure"
    end
    machine.vm.provision :ansible_local do |ansible|
      ansible.playbook          = "playbook.yml"
      ansible.provisioning_path = "/home/vagrant/ansible"
      ansible.verbose           = true
      ansible.install           = true
      ansible.limit             = "all" # or only "nodes" group, etc.
      ansible.inventory_path    = "inventory"
    end
  end

end


