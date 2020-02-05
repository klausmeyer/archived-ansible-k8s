# -*- mode: ruby -*-
# vi: set ft=ruby :

MACHINES = %w(k8s-node01 k8s-node02 k8s-node03)

Vagrant.configure("2") do |config|
  MACHINES.each do |name|
    config.vm.define name do |machine|
      machine.vm.box = "debian/buster64"
      machine.vm.hostname = name

      machine.vm.provider :libvirt do |v|
        v.cpus = 2
        v.memory = 2048
        v.storage :file, size: '20G', type: 'qcow2', device: 'vdb'
      end

      machine.vm.synced_folder ".", "/vagrant", disabled: true

      # Only execute once the Ansible provisioner,
      # when all the machines are up and ready.
      if name == MACHINES.last
        machine.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.playbook = "playbook.yml"
          ansible.become = true
          ansible.compatibility_mode = "2.0"

          ansible.groups = {
            "k8s"              => MACHINES,
            "k8s_master"       => MACHINES.take(1),
            "k8s_worker"       => MACHINES.drop(1),
            "glusterfs"        => MACHINES,
            "glusterfs_master" => MACHINES.take(1),
          }
        end
      end
    end
  end

end
