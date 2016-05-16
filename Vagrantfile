# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure '2' do |config|
  # Test machines
  # -------------

  # These test machines will configure the installation with all
  # its extensions enabled, in order to test the validity
  # of the role.

  # Ubuntu machines are available:
  # - "test-ubuntu-precise"
  # - "test-ubuntu-trusty"
  # - "test-ubuntu-xenial"
  # OSX machines are available:
  # - "test-osx-elcapitan"

  def apply_test_ansible_defaults(ansible)
    ansible.playbook       = './test.yml'
    ansible.inventory_path = './inventory'
  end

  config.vm.define 'test-osx-elcapitan', autostart: false do |box|
    box.vm.box = 'jhcook/osx-elcapitan-10.11'
    config.vm.network :private_network, ip: '192.168.33.23'
    config.vm.provision :ansible do |ansible|
      apply_test_ansible_defaults ansible
      ansible.extra_vars = {}
    end
  end

  config.vm.define 'test-ubuntu-xenial', autostart: false do |box|
    box.vm.box = 'ubuntu/xenial64'
    # config.vm.network :private_network, ip: '192.168.33.22'
    # due to issue https://github.com/mitchellh/vagrant/issues/6871
    # in vagrant 1.8.1 we'll use loopback interface and static port for ssh
    config.vm.network 'forwarded_port', guest: 22, host: 22_221
    config.vm.provision :shell, inline: 'apt-get update &&\
      apt-get install libnss-myhostname python -y'
    config.vm.provision :ansible do |ansible|
      apply_test_ansible_defaults ansible
      ansible.extra_vars = {}
      ansible.verbose = 'v'
    end
  end

  config.vm.define 'test-ubuntu-trusty', autostart: false do |box|
    box.vm.box = 'ubuntu/trusty64'
    config.vm.network :private_network, ip: '192.168.33.21'
    config.vm.provision :ansible do |ansible|
      apply_test_ansible_defaults ansible
      ansible.extra_vars = {}
    end
  end

  config.vm.define 'test-ubuntu-precise', autostart: false do |box|
    box.vm.box = 'ubuntu/precise64'
    config.vm.network :private_network, ip: '192.168.33.20'
    config.vm.provision :ansible do |ansible|
      apply_test_ansible_defaults ansible
      ansible.extra_vars = {}
    end
  end
end
