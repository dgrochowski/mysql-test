CONF_IP = '10.0.0.200'
MACHINE_NAME = 'dev-current'

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'virtualbox'
Vagrant.configure("2") do |config|
  config.vm.box = "debian/jessie64"

  config.vm.network :private_network, ip: "#{CONF_IP}"
  config.ssh.forward_agent = true

  # Customize your VM parameters
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--memory", 1024]
    #vb.customize ["modifyvm", :id, "--name", "#{MACHINE_NAME}"]
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", "80"]
    vb.customize ["modifyvm", :id, "--cpus", "1"]
    config.vm.post_up_message = "Machine is ready to use on #{CONF_IP}"
  end

  config.vm.synced_folder "./", "/var/www/current", id: "vagrant-root", type: "nfs"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
  end
end
