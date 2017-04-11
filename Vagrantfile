# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.require_version ">= 1.8.0"

# Install required Vagrant plugins
missing_plugins_installed = false
required_plugins = %w(vagrant-vbguest vagrant-hostmanager vagrant-cachier vagrant-registration vagrant-adbinfo landrush vagrant-sshfs)

required_plugins.each do |plugin|
  if !Vagrant.has_plugin? plugin
    system "vagrant plugin install #{plugin}"
    missing_plugins_installed = true
  end
end

# If any plugins were missing and have been installed, re-run vagrant
if missing_plugins_installed
  exec "vagrant #{ARGV.join(" ")}"
end


Vagrant.configure(2) do |config|

  config.vm.box = "precise32"

  config.vm.provider "libvirt" do |v|
     v.driver = "kvm"
     v.memory = 2048
     v.cpus   = 1
  end

  #config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM:
  #  vb.memory = 2048
  #  vb.cpus = 1
  #  vb.name = "nexus"

    # Enable VB performance customizations
  #  vb.customize ["modifyvm", :id, "--ioapic", "on"]
  # end
  

  # config.vm.hostname = "nexus.vm"
  # config.vm.network "private_network", ip: "10.1.2.4"

  config.vm.define :nexus do |nexus|
    nexus.vm.network :private_network, :ip => "192.168.42.50"
      # Config landrush DNS
    #config.landrush.enabled = true
    #config.landrush.tld = "nexus-libvirt.vm"
    #config.landrush.host_ip_address = "10.1.2.4"
    #config.landrush.guest_redirect_dns = false
    #config.landrush.upstream "8.8.8.8" #Google DNS
    
    # Optional. Allows to sync Nexus work folder to the host machine.
    config.vm.synced_folder "./nexus", "/srv/sonatype-work/nexus", create: true, :mount_options => ["uid=998,gid=998"]

    #config.vm.synced_folder "./nexus", "/srv/sonatype-work/nexus", type: "sshfs"

    config.vm.provision :puppet do |puppet|
       puppet.manifests_path = "puppet/manifests"
       puppet.module_path = "puppet/modules"
     end
  	
    config.vm.provision "shell", inline: "service nexus restart", run: "always"
    config.vm.post_up_message = "http://192.168.42.50:8081/nexus/"
  end

end
