# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

  config.vm.box = "centos7"

  config.vm.define "maquina1", autostart: true do |maquina1|
    maquina1.vm.network "public_network", bridge: "en0: Ethernet"
    config.vm.network "forwarded_port", guest: 3000, host: 3000
#    maquina1.vm.network "public_network", bridge: "en1: Wi-Fi (AirPort)"
  end


  config.vm.define "maquina2", autostart: true do |maquina2|
    maquina2.vm.network "public_network", bridge: "en0: Ethernet"
  end

end
