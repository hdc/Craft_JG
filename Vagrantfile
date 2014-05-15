# -*- mode: ruby -*-
# vi: set ft=ruby :

# ------------------------------------------------------------------------
# CONFIGURABLE PROPERTIES
# ------------------------------------------------------------------------
$hostname  = 'craft.dev'
$ip = '192.168.11.11'
# ------------------------------------------------------------------------

Vagrant.configure('2') do |config|
  # Basics
  config.vm.box     = 'precise64'
  config.vm.box_url = 'http://files.vagrantup.com/precise64.box'

  # Networking.
  config.vm.hostname = $hostname
  config.vm.network :private_network, ip: $ip

  # Provisioning.
  config.vm.provision :shell, :path => 'puppet/bootstrap/bootstrap.sh'

  config.vm.provision :puppet do |puppet|
    puppet.facter = {
      'hostname' => $hostname
    }

    puppet.manifest_file  = 'init.pp'
    puppet.manifests_path = 'puppet/manifests'
    puppet.module_path    = 'puppet/modules'
  end

  #memeory
    config.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 2
    end

  # Shared folders:
  config.vm.synced_folder "craft/app", "/vagrant/craft/app",
    :owner => 'www-data',
    :group => 'www-data',
    :mount_options => ['dmode=777,fmode=777']

  config.vm.synced_folder "craft/config", "/vagrant/craft/config",
    :owner => 'www-data',
    :group => 'www-data',
    :mount_options => ['dmode=777,fmode=777']

  config.vm.synced_folder "craft/storage", "/vagrant/craft/storage",
    :owner => 'www-data',
    :group => 'www-data',
    :mount_options => ['dmode=777,fmode=777']

   config.vm.synced_folder "public/uploads", "/vagrant/public/uploads",
       :owner => 'www-data',
       :group => 'www-data',
       :mount_options => ['dmode=777,fmode=777']
end

