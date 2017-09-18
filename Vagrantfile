# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure('2') do |config|
  config.vm.box = 'fedora/24-cloud-base'

  config.vm.network 'forwarded_port', guest: 3000, host: 3000
  config.vm.network 'forwarded_port', guest: 4000, host: 4000
  config.vm.network 'forwarded_port', guest: 1080, host: 1080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network 'private_network', ip: '192.168.33.13'

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network 'public_network'

  config.vm.hostname = 'devbox'

  config.vm.synced_folder './ansible', '/home/vagrant/ansible'
  config.vm.synced_folder './apps', '/home/vagrant/apps'

  config.vm.provider 'virtualbox' do |vb|
    vb.name = 'DevBox'
    vb.gui = false
    vb.memory = '2048'
  end

  config.ssh.forward_agent = true

  config.vm.provision 'shell', inline: 'sudo ansible-galaxy install git+https://github.com/JakovlevDS/ansible-rbenv-role.git,5439b936af82681567d3f9b63d3bf4fa11ad524a', privileged: false

  config.vm.provision 'ansible_local' do |ansible|
    ansible.provisioning_path = '/home/vagrant'
    ansible.playbook = 'ansible/vagrant.yml'
    ansible.verbose = false # 'vvvv'
  end
end
