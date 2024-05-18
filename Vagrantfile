# -*- mode: ruby -*-
# vi: set ft=ruby :

require "etc"

# Change this to your SSH public key path
PUBLIC_KEY_PATH = "CHANGEME".freeze

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04-arm64"

  # Prevent mounting of local directory into vm
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provision "shell" do |shell|
    shell.inline = <<~DOC
      # Allow us to SSH using our public key rather than using `vagrant ssh`
      echo '#{IO.read(PUBLIC_KEY_PATH)}' >> /home/vagrant/.ssh/authorized_keys
    DOC
  end

  config.vm.provider "vmware_desktop" do |v|
    # Use the bare minimum amount of RAM
    v.vmx["memsize"] = "768"

    # Set CPUs to half the cores detected by Ruby, which should work best in
    # most cases
    v.vmx["numvcpus"] = (Etc.nprocessors / 2.0).ceil
  end

  # Define the VMs
  config.vm.define "remote0" do |m|
    m.vm.hostname = "remote0"
    m.vm.network "private_network", ip: "10.0.0.2"
  end

  config.vm.define "remote1" do |m|
    m.vm.hostname = "remote1"
    m.vm.network "private_network", ip: "10.0.0.3"
  end
end
